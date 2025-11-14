+++
author = "Thomas Evensen"
title = "Architecture"
date = "2025-11-14"
tags = ["architecture","AI"]
categories = ["architecture"]
+++

Over the past five years, I have dedicated approximately 5,800 commits to the RsyncUI GitHub repository. This substantial number of commits demonstrates the significant learning curve I have experienced while developing RsyncUI. The foundation of RsyncUI was the now-archived project RsyncOSX. The primary distinction between these two projects lies in the adoption of SwiftUI, as well as the evolution and enhancement of Swift as a programming language to its current version.

Having retired from my professional career three and a half years ago, I have dedicated myself to developing RsyncUI several days a week. While I also engage in various hobbies such as bird photography, training, cross-country skiing, and spending time with my children and grandchildren, the continuous development of RsyncUI remains a primary focus throughout the year.

I am consistently expanding my knowledge of Swift and SwiftUI through reading blogs and, in recent times, utilizing artificial intelligence in the development process.

Why continue working on RsyncUI? My primary motivation stems from my passion for Swift development. As long as there are users globally utilizing RsyncUI, I will persist in maintaining and enhancing its functionality. Additionally, I personally use RsyncUI to secure my own data. The command-line tool rsync is a well-proven and stable synchronization tool, and building a GUI on top of rsync is a very grateful task.

I inquired about an analysis of the RsyncUI GitHub repository from AI, specifically Warp and GPT 5.1 (Low reasoning). Below is the response, which is copied and pasted (no changes, only removal of some details).

### GPT 5.1 analyse of RsyncUI

Key features:

- **Sidebar menu** (`Sidebaritems`) determines which “mode” you’re in: sync, tasks, rsync parameters, verify, snapshots, logs, restore, profiles.
- **Context-sensitive menu**:
  - Snapshots only shown if there are snapshot tasks.
  - Restore only shown if there are remote tasks (and `rsyncversion3` supports it).
  - Verify remote only shown when allowed by config and global flags.
- **Profile picker** in sidebar and in toolbar, depending on column visibility.
- Deep link `handleURLsidebarmainView` supports:
  - Quicktask.
  - Load profile.
  - Load profile and estimate.
  - Load profile and verify (for external URLs).
- **Volume observer**:
  - Watches mounting/unmounting of drives, tries to switch profile automatically if a matching offline-volume-based profile is detected.

### Tasks view and toolbar integration

`TasksView` is the primary synchronization screen:

- Shows a list (`ListofTasksMainView`) with tasks for the current profile.
- Maintains `selecteduuids`, `selectedconfig`, and various focus states (to respond to keyboard shortcuts from menu commands).
- Syncs with `ProgressDetails` to show estimates and decide what to execute.
- Toolbar buttons:
  - **Estimate** (wand icon) → pushes `Tasks(task: .summarizeddetailsview)` into `executetaskpath`.
  - **Run** (play icon) → either executes estimated tasks or prompts to run all tasks without estimate.
  - **Reset** (clear).
  - Extended toolbar (when `showquicktask` is true): quick “view output”, “view log file”, quick synchronize, charts, calendar, open floating rsync output window.
  - **Deep link** actions via yellow “bolt.shield” icons.

Core execution decision logic:

```swift path="/Users/thomas/RsyncUI/RsyncUI/Views/Tasks/TasksView.swift" start=491 end=507
func execute() {
    rsyncUIdata.executetasksinprogress = true
    if selecteduuids.count == 0,
       progressdetails.alltasksestimated(rsyncUIdata.profile) == true {
        // Execute all estimated tasks
        selecteduuids = progressdetails.getuuidswithdatatosynchronize()
        executetaskpath.append(Tasks(task: .executestimatedview))
    } else if selecteduuids.count >= 1,
              progressdetails.tasksareestimated(selecteduuids) == true {
        // Execute only estimated selected tasks
        selecteduuids = progressdetails.getuuidswithdatatosynchronize()
        executetaskpath.append(Tasks(task: .executestimatedview))
    } else {
        // Execute all tasks, no estimate: show confirm alert
        showingAlert = true
    }
}
```
The actual navigation and presentation of “execute estimated view”, “one task details”, etc. are handled in other views such as `SidebarTasksView`, `SummarizedDetailsView`, `EstimateTableView`, etc.

---

## Concurrency and async patterns

RsyncUI is written with **modern Swift concurrency**:

- `@MainActor` applied to UI-facing classes (`Rsyncversion`, `PrepareParameters`, `SSHPrepareParameters`, `EstimateExecute`, `UserConfiguration`).
- **Actors** for I/O and log handling (`ActorLogToFile`, `ActorReadSynchronizeConfigurationJSON`, etc.) to avoid data races.
- `Task { ... }` blocks in views to perform asynchronous operations on appear and on change.
- The `RsyncProcess` handlers are largely asynchronous and push updates via closures and `ActorLogToFile`.

Design consequences:

- Long-running jobs (rsync, file I/O) do not block the main thread.
- UI remains responsive, with progress and status updates coming through observed state.
- Use of `weak var localprogressdetails` ensures the execution engine doesn’t retain UI state strongly.

---

## Scheduling, deep links, and advanced features

### Scheduling

- `GlobalTimer.shared` manages in-app schedules:
  - Next scheduled date display.
  - Triggering scheduled profile execution, which piggybacks on deep-link URL handling (`.loadprofileandestimate`).
- `ReadSchedule` and `WriteSchedule` manage JSON-based schedule storage.
- `CalendarMonthView`, `CalendarDayView` present scheduled runs in the UI.

### Deep links and automation

`DeeplinkURL` + `handleURLsidebarmainView` supports:

- External apps (or scripts) can call `RsyncUI` with URLs like:
  - `rsyncui://quicktask`
  - `rsyncui://loadprofile?profile=Default`
  - `rsyncui://loadprofileandestimate?profile=Default`
  - `rsyncui://loadprofileandverify?profile=Default&id=<backupID>`
- Internal toolbar also uses deep link paths to unify code paths for “Estimate & Synchronize” and verify flows.

---

## Tooling, style, and ecosystem

Even though we didn’t inspect every file:

- There are config files for **SwiftLint** (`.swiftlint.yml`) and **Periphery** (`.periphery.yml`) → indicates attention to code quality and dead code detection.
- Uses **Observation** framework (`@Observable`, `@Bindable`) rather than classic `ObservableObject`, aligning with modern SwiftUI patterns.
- **External libraries** used:
  - `RsyncProcess` – encapsulates running `rsync` as a process.
  - `RsyncArguments` – builds argument arrays from configuration structs.
  - `ParseRsyncOutput` – parsing rsync output into statistics objects.
- Widgets (`WidgetEstimate`, `WidgetVerify`) consume the same stored configuration/log data, providing quick-glance UI in macOS widgets.

---

## Design strengths and potential improvements

### Strengths

- **Clear separation of concerns**:
  - Views → layout and user interactions.
  - Model layer → rsync orchestration, configuration, scheduling, parsing.
  - Infrastructure → JSON storage, logging, widgets, XPC.
- Good use of **Swift concurrency** and **actors** to keep file and process I/O safe and non-blocking.
- **Extensible task model** (`SynchronizeConfiguration`) with snapshot, SSH, and daemon support.
- Deep integration with **macOS features**:
  - NavigationSplitView, menu commands, deep link URLs, mounted volume notifications.
  - Widgets and XPC.
- Strong focus on **rsync correctness**:
  - Distinction between v3 and openrsync.
  - Output trimming and tagging validation.
  - A clear estimate-before-execute workflow.

### Possible improvements / observations

These are not criticisms but areas you might refine if you extend or learn from the project:

1. **Global singleton usage**  
   `SharedReference` is a classic global singleton with many responsibilities. It works, but:
   - Injecting a smaller “environment” or “settings” struct might make some components easier to unit test.
   - Some boolean flags might be better grouped (e.g., network/options, UI preferences, rsync environment).

2. **Configuration and JSON type-safety**  
   - There is a three-layer structure: Decode* → domain struct → SharedReference.
   - You might consider strongly typed enums for some integers (e.g., `rsyncversion3` as an enum instead of Int -1/1) to reduce magic numbers.

3. **Complexity in `SidebarMainView` and `TasksView`**  
   - These two views handle a lot of behavior: scheduling, volume detection, deep links, navigation, toolbar logic.
   - Further factoring into smaller view models or dedicated coordinator types could make each part easier to reason about.

4. **EstimateExecute complexity**  
   - `EstimateExecute` is well-structured but long and multi-purpose (estimate, execute with estimate, execute without estimate).
   - Splitting into separate types (e.g., `Estimator`, `Executor`, `NoEstimationExecutor`) sharing a base helper might clarify responsibilities.

---

## How to think about this app as a template

If you’re trying to learn from RsyncUI for your own projects, key patterns to copy:

- **Model-first design**: define your equivalent of `SynchronizeConfiguration` and domain structs clearly, then build UI around them.
- Use **actors** for any file/network/process I/O and keep UI updates on the main actor.
- Isolate “external process orchestration” behind a type like `EstimateExecute` that:
  - Accepts domain models as input.
  - Uses callbacks / bindings to feed progress into the UI.
  - Handles all process lifecycle and logging internally.
- Use **SwiftUI with NavigationSplitView** and state-enriched sidebars for complex tool-like macOS apps.
