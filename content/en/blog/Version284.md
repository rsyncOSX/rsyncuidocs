+++
author = "Thomas Evensen"
title = "Version 2.8.4"
date = "2025-12-26"
tags = ["changelog","version 2.8.4"]
categories = ["changelog"]
+++

### Version 2.8.4 - Dec 26, 2025

Version 2.8.4rc2 has been released as the new version, with no new builds released.

<div class="alert alert-secondary" role="alert">

In version 2.8.2, there is an issue with the "empty stats file". For more information, please refer to last on this page. I believe I have identified the cause of this issue. The previous *RsyncProcess* utilize AsyncSequence (AsyncStream), which is part of version 2.8.2, a feature that continuously listens for data. A few days ago, I modified parts of the new *RsyncProcessStreaming* package to try it as well. AsyncSequence is a robust concurrency feature, but attempting to use it in the new package caused the "empty stats file" issue again. 

</div>

<div class="alert alert-danger" role="alert">
  
Version, 2.8.4 incorporates the version of the *RsyncProcessStreaming* package that eliminates the occurrence of the "empty stats file". 

</div>

I am uncertain as to why the AsyncStream encounters issues with the aforementioned problem. Nevertheless, I intend to investigate and determine if I can resolve this issue for my own learning and interest. Specifically, I will implement a mechanism to halt the process and drain any remaining data before the termination task is executed.

### Major Features & Improvements

- **Total Commits (git) Since 2.8.2**: 137+
- **Development Period**: December 12-24, 2025

#### 🔄 RsyncProcessStreaming Migration - Complete
- **Unified Process Execution Model**: All process execution now uses the `RsyncProcessStreaming` package for event-driven, streaming process handling
- **Simplified Handler Management**: Introduced `ProcessHandlers` factory with built-in cleanup hooks to prevent memory leaks and retain cycles
- **Real-time Output Streaming**: Process output is now streamed in real-time, enabling immediate UI updates and better user feedback
- **Files Updated**: Estimate.swift, Execute.swift, RestoreTableView.swift, OneTaskDetailsView.swift, ExecutePushPullView.swift, VerifyTasks.swift

#### 📦 ParseRsyncOutput Swift Package Integration
- **Extracted rsync output parsing** into a reusable Swift Package for improved code reusability and testability
- **Unified parsing logic** across all rsync output processing operations
- **Package repository**: [ParseRsyncOutput](https://github.com/rsyncOSX/ParseRsyncOutput)

#### ✅ Comprehensive Testing Framework
- **New RsyncUITests target** added with initial test suite
- **UI tests** for arguments and deeplink URLs
- **Output processing tests** covering:
  - Tail trimming (20-line limit)
  - Directory line filtering
  - Error detection patterns
  - Malformed/empty output edge cases

### Core Changes

#### Process Execution & Streaming
- Refactored `ObservableRestore` to use `RsyncProcessStreaming`
- Refactored task verification to use streaming process handlers
- Added streaming support to QuicktaskView
- Refactored rsync version check to use streaming process
- Remove RsyncProcess dependency - replaced with RsyncProcessStreaming
- Streaming handler cleanup refactoring to prevent retain cycles and memory leaks

#### UI/UX Enhancements
- **Improved UI feedback** for task progress and completion
- **Enhanced progress view** with better styling and layout
- Added configuration table view to ProfileView
- Renamed table column from 'Time' to 'Time last' across multiple views
- Refactored profile deletion UI in ProfileView
- Improved help text for --delete parameter usage
- Better handling of hiddenID in Estimate and Execute operations
- Removed RsyncRealtimeView and related obsolete UI references

#### Code Quality & Refactoring
- **Refactor optional handling patterns** with guard-chain flattening and single binding for counts
- **Refactor enum cases** to camelCase: RsyncCommand, PushPullCommand, OtherRsyncCommand, PlanSnapshots, DayOfWeek
- **Variable naming improvements** for consistency and clarity across codebase
- **Removed unnecessary whitespace** and improved code formatting
- **SwiftLint configuration updates** and inline rule directives
- **Refactored UI views** for improved readability (AddTaskView, SidebarMainView, TasksView, QuicktaskView)
- **Refactored parameter field handling** in configuration models with optional fields

#### Configuration & Settings
- **New argument validation feature**: Added toggle for argument validation in execution flow
- Added 'validate arguments' setting to user configuration
- Improved argument validation with nil checks and proper error handling
- Add dry-run validation to argument checks
- Configuration model improvements with optional parameter handling

#### Logging & Debugging
- Refactored and cleaned up logging and test code
- Removed rsync output logfile support from log views
- Gated per-line streaming logs behind DEBUG flag
- Added debug threading check for streaming handlers
- Silenced debug print statements in streaming handlers
- Improved logging to use `errorMessageOnly` with better formatting

#### Dependencies & Version Updates
- Updated all Swift package dependencies to main branch

### Bug Fixes & Stability
- Fixed guard statement order and typo in snapshot and restore operations
- Safely unwrap streamingHandlers before use
- Remove unnecessary `[weak self]` in processTermination handlers
- Made parameter4 optional to better handle delete flag
- Fix potential nil issues in argument execution

### Architecture Improvements
- **Unified streaming architecture** with simplified process lifecycle
- **Improved memory management** through explicit cleanup patterns
- **Enhanced testability** with extracted ParseRsyncOutput package
- **Better separation of concerns** through handler factory pattern

## Dependencies Updated
- RsyncProcessStreaming (streaming process execution)
- ParseRsyncOutput (output parsing and processing)
- RsyncArguments (rsync command arguments)
- RsyncProcess (legacy - being phased out in favor of streaming)

## Empty stats file

The process termination signal indicates that the external rsync process has completed and the process has been terminated. All tasks within the main synchronize view are updated with the latest run, but there is also a separate logging that records the main result of each task with a timestamp.

Occasionally, when synchronizing a small amount of data, the termination signal is detected before all output from rsync has been drained. In such cases, the separate logging may be missing. The process termination signal serves as a message to perform logging, but if the last summarized rsync output is missing, there is nothing to log. 

*Output from rsync* refers to the information that rsync provides to the terminal during the execution of a task.

<div class="alert alert-danger" role="alert">

If RsyncUI detects an empty statistics file, it will append a default log record stating `0 files : 0.00 MB in 0.00 seconds`.

</div>

If logging fails due to the aforementioned reason, this error will be generated, if *enabled*.

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}

