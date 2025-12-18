+++
author = "Thomas Evensen"
title = "RsyncProcess vs RsyncProcessStreaming"
date = "2025-12-16"
tags = ["version 2.8.4"]
categories = ["technical details"]
+++

**RsyncProcessStreaming** is the superior implementation and should be preferred for new code. It offers a simpler architecture, better resource management, proper handling of streaming data, and cleaner error handling compared to the original RsyncProcess.

---

## Key Differences & Benefits

### 1. Simpler, More Modern Architecture

#### RsyncProcess (Original)
Uses a complex notification-based approach:
- Multiple async tasks monitoring NotificationCenter notifications
- Manual coordination between `sequenceFileHandlerTask` and `sequenceTerminationTask`
- Complex state management with flags like `hasSeenSummaryStart`, `isRealRun`, `isVersionProbe`
- Requires manual notification triggering with `waitForDataInBackgroundAndNotify()`

#### RsyncProcessStreaming (Improved)
Uses direct callbacks:
- Clean `readabilityHandler` closures on file handles
- Single `terminationHandler` for process completion
- Minimal state tracking (just `lineCounter`)
- System handles notification automatically

**Benefit**: Less code, fewer moving parts, easier to understand and debug.

---

### 2. Better Resource Management

#### RsyncProcess Issues
```swift
// Manual draining loop in termination
try? await Task.sleep(nanoseconds: 50_000_000)
var totalDrained = 0
while true {
    let data: Data = pipe.fileHandleForReading.availableData
    if data.isEmpty {
        break
    }
    totalDrained += data.count
    // Process data...
}
```
- Data can be lost between notification delivery and processing
- Arbitrary 50ms sleep before draining
- Complex task cancellation coordination

#### RsyncProcessStreaming Solution
```swift
process.terminationHandler = { task in
    outputPipe.fileHandleForReading.readabilityHandler = nil
    errorPipe.fileHandleForReading.readabilityHandler = nil
    
    if let trailing = await accumulator.flushTrailing() {
        deliverLine(trailing)
    }
    // Clean termination...
}
```
- Automatic cleanup when handlers are set to `nil`
- No artificial delays needed
- Proper handling of any trailing data

**Benefit**: More reliable, no data loss, cleaner shutdown.

---

### 3. Proper Output Buffering

#### RsyncProcess Problem
```swift
str.enumerateLines { line, _ in
    self.output.append(line)  // What if line is incomplete?
}
```
Appends directly to output array without handling partial lines that may span multiple data chunks.

#### RsyncProcessStreaming Solution
```swift
actor StreamAccumulator {
    private var partialLine: String = ""
    
    func consume(_ text: String) -> [String] {
        let combined = partialLine + text  // Handles splits mid-line
        let parts = combined.components(separatedBy: .newlines)
        partialLine = parts.last ?? ""  // Preserves incomplete line
        let newLines = parts.dropLast().filter { !$0.isEmpty }
        lines.append(contentsOf: newLines)
        return Array(newLines)
    }
    
    func flushTrailing() -> String? {
        guard !partialLine.isEmpty else { return nil }
        let trailing = partialLine
        partialLine = ""
        lines.append(trailing)
        return trailing
    }
}
```

**Benefit**: Correctly handles streaming data where lines can be split across multiple reads.

---

### 4. Cleaner Error Handling

#### RsyncProcess
- Manually checks errors line-by-line with `errorDiscovered` flag
- stderr goes to same pipe as stdout (mixed output)
- Error logging is conditional and complex
- No structured error information

#### RsyncProcessStreaming
```swift
let outputPipe = Pipe()
let errorPipe = Pipe()  // Separate pipe for errors
process.standardOutput = outputPipe
process.standardError = errorPipe

// Dedicated error accumulation
errorPipe.fileHandleForReading.readabilityHandler = { handle in
    // ... record errors separately ...
    await accumulator.recordError(text)
}

// Structured error on failure
if task.terminationStatus != 0 {
    self?.handlers.propagateError(
        RsyncProcessError.processFailed(
            exitCode: task.terminationStatus,
            errors: errors
        )
    )
}
```

**Benefit**: Better error diagnostics, separation of stdout/stderr, structured error types.

---

### 5. Removed Unnecessary Complexity

#### RsyncProcess Special Cases
- Version probe detection (`isVersionProbe`)
- Different handlers for rsync3 vs openrsync:
  - `handleRsync3Data()`
  - `handleOpenRsyncData()`
  - `handleVersionData()`
- Summary detection logic (`hasSeenSummaryStart`, `summaryStartMarker`)
- Conditional file handler updates based on dry-run detection
- Complex flag management throughout

#### RsyncProcessStreaming
- Single consistent data handling path
- No version-specific logic
- Simpler, more predictable behavior
- Easy to extend if needed

**Benefit**: Lower maintenance burden, fewer edge cases, easier to reason about.

---

### 6. Thread Safety & Concurrency

#### RsyncProcess
```swift
@MainActor
public final class RsyncProcess {
    // Entire class runs on main thread
}
```
- Forces all processing onto main thread
- Can cause UI blocking with heavy output
- Less efficient use of system resources

#### RsyncProcessStreaming
```swift
public final class RsyncProcess {
    // Not bound to main actor
    
    outputPipe.fileHandleForReading.readabilityHandler = { handle in
        Task.detached {  // Process off main thread
            let lines = await accumulator.consume(text)
            
            for line in lines {
                // Only dispatch to main when needed
                Task { @MainActor in
                    self.handlers.fileHandler(self.lineCounter)
                }
            }
        }
    }
}
```
- Uses `Task.detached` for data processing
- Only dispatches to `@MainActor` when calling handlers
- Thread-safe with `actor StreamAccumulator`

**Benefit**: Better performance, no UI blocking, proper use of Swift concurrency.

---

### 7. More Predictable Data Flow

#### RsyncProcess Flow
```
Data Available
    ↓
Post Notification
    ↓
NotificationCenter delivers to AsyncSequence
    ↓
Task processes notification
    ↓
Manual call to waitForDataInBackgroundAndNotify()
    ↓
Repeat
```

#### RsyncProcessStreaming Flow
```
Data Available
    ↓
readabilityHandler called automatically
    ↓
Process data
    ↓
Done (system continues monitoring)
```

**Benefit**: Simpler mental model, fewer opportunities for bugs.

---

## Side-by-Side Comparison

| Feature | RsyncProcess | RsyncProcessStreaming |
|---------|--------------|----------------------|
| **Architecture** | Notification-based | Callback-based |
| **Lines of Code** | ~350 | ~180 |
| **State Flags** | 6+ flags | 1 counter |
| **Async Tasks** | 2 coordinated tasks | 0 (uses handlers) |
| **Thread Model** | @MainActor (blocking) | Detached + targeted @MainActor |
| **Partial Line Handling** | ❌ No | ✅ Yes |
| **Separate stderr** | ❌ No | ✅ Yes |
| **Error Structure** | Generic Error | RsyncProcessError with details |
| **Version-Specific Code** | ✅ Yes | ❌ No (simpler) |
| **Manual Draining** | ✅ Yes (with delay) | ❌ No (automatic) |
| **Maintenance Complexity** | High | Low |

---

## When You Might Still Use RsyncProcess

The only scenarios where the original might be preferred:

1. **Summary Suppression**: If you specifically need the `isRealRun` and `hasSeenSummaryStart` logic to suppress final summary lines during progress reporting
2. **Version-Specific Behavior**: If you need different behavior for openrsync vs rsync3

**However**: These features can easily be added to RsyncProcessStreaming if needed, and the architecture is much cleaner for doing so.

---

## Migration Considerations

If migrating from RsyncProcess to RsyncProcessStreaming:

1. **Handler Compatibility**: Both use the same `ProcessHandlers` protocol, so handlers are compatible
2. **Output Array**: Both accumulate output, accessible via `StreamAccumulator.snapshot()`
3. **Error Checking**: Similar pattern, but streaming version has better error details
4. **No Breaking Changes**: API is nearly identical for consumers

---

## Recommendation

### ✅ Use RsyncProcessStreaming

**Reasons:**
- Has fewer bugs and edge cases
- Is easier to maintain and modify
- Handles streaming data correctly
- Has better separation of concerns
- Uses modern Swift concurrency properly
- Is more efficient (no polling, no artificial delays)
- Better error reporting with separate stderr
- Less code to understand and debug

---

## Conclusion

The original **RsyncProcess** appears to have evolved with accumulated complexity over time, with features and flags added as needs arose. 

**RsyncProcessStreaming** is a cleaner redesign that learned from those lessons, removing unnecessary complexity while adding proper streaming support and better error handling.

For any new code, **RsyncProcessStreaming is strongly recommended**. For existing code using RsyncProcess, consider migrating when practical, as the benefits in maintainability and reliability are substantial.