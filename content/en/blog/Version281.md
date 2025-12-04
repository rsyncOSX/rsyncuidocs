+++
author = "Thomas Evensen"
title = "Version 2.8.1"
date = "2025-12-04"
tags = ["changelog","version 2.8.1"]
categories = ["changelog"]
+++

### Version 2.8.1 (build 172) - Dec 4, 2025 Release Candidate 1 (RC1)

An AI-generated changelog is available at the bottom of this page. Some info about the *no stats, no log* issue.

The RC1 has been *updated*, and all annoying messages regarding missing files should be resolved. This release candidate will be upgraded to a new maintenance release tomorrow, provided that no bugs are identified within the *next 24 hours*.

There are both positive and negative aspects to consider. On the positive side, I have successfully identified the occurrence of the issue and can notify the user accordingly. However, I am **unable** to modify the `try? await Task.sleep(nanoseconds: sleeptime)` code to resolve the problem. To be candid, I am somewhat lost why this issue arises. Nevertheless, the positive aspect is that RsyncUI is actively notifying the user, and the user has the ability to initiate a synchronization manually when the issue occurs. 

*In the upcoming maintenance release, version 2.8.1, an alert will be introduced to notify users when RsyncUI detects a lack of data to write logdata.*

<div class="alert alert-danger" role="alert">

The alert is currently disabled by default in version 2.8.1. However, version 2.8.2 will introduce an option to enable it. If RsyncUI detects an empty statistics file, it will append a default log record stating `0 files : 0.00 MB in 0.00 seconds`.

If you encounter this issue, the data is synchronized, but RsyncUI alerts about a missing loggdata file. For your safety confirm data synchronization, perform another estimate and execute or force an execute without estimation.

</div>

If logging fails due to the aforementioned reason, this error will be generated (in version 2.8.2).

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}

## Release Notes: v2.8.0 → v2.8.1rc1

### Overview
This release cycle includes 25 commits across 32 files, focusing on stability improvements, architectural refactoring, and enhanced error handling. The release emphasizes code maintainability and robustness.

**Stats:** 526 insertions(+), 386 deletions(-)

---

### 🏗️ Architectural Improvements

#### Execution Logic Refactoring
- [x] Split `EstimateExecute.swift` into separate `Estimate.swift` and `Execute.swift` files
- [x] Cleaned up initialization logic and removed convenience initializers
- [x] Improved separation of concerns between estimation and execution phases
- [x] Refactored EstimateExecute initialization logic

#### Error Handling & Robustness
- [x] Enhanced error handling in `RemoteDataNumbers` initialization
- [x] Added fallback mechanisms for missing stats with default values
- [x] Improved error catching in log record handling
- [x] Added conditional error handling when appending default stats to logs
- [x] Refactored error handling and logging method names

#### Code Cleanup
- [x] Removed network monitoring feature and related code
- [x] Removed sleeptime setting and configuration (after initial addition, then reverted)
- [x] Removed WidgetVerify extension and related files
- [x] Removed verify URL support and related code
- [x] Cleaned up unused code in estimation initialization

---

### 📊 Logging & Monitoring Enhancements

#### Advanced Logging System
- [x] Refactored log record handling with improved error catching
- [x] Added conditional logging for summary log records
- [x] Added debug logging for `getstats()` success and failure tracking
- [x] Added commented-out function for permanent log storage (future feature)
- [x] Improved rsync output parsing to use `getstats()` with comprehensive error handling
- [x] Updated `Logging.swift` with enhanced functionality

#### Log Settings
- [x] Updated `ObservableLogSettings.swift` with refined configurations
- [x] Enhanced log file handling in storage actors
- [x] Improved `ActorReadLogRecordsJSON.swift` error handling

---

### 🎨 UI & Progress Tracking

#### Progress View Improvements
- [x] Extracted `SynchronizeProgressView` to separate file for better modularity
- [x] Added `RestoreProgressView` for improved progress display during restore operations
- [x] Set max value on dry run in restore and quicktask operations
- [x] Refactored progress view with max value support
- [x] Improved UI progress indicators and logging

#### View Enhancements
- [x] Increased minHeight for sheet views in `TasksView`
- [x] Refactored URL estimate button logic in `AddTaskView`
- [x] Updated query item handling in `SidebarTasksView`
- [x] Updated estimation in progress view

---

### 🔧 Process & Configuration Management

#### Path & Catalog Handling
- [x] Fixed config path concatenation in `Homepath`
- [x] Refactored catalog and volume models and services
- [x] Updated catalog path logic and progress handling
- [x] Added `sharedPathForRestore` to Params with formatted restore arguments
- [x] Refactored path concatenation and alert handling

#### Process Management
- [x] Refactored RsyncProcess termination configuration
- [x] Improved TCPconnections handling
- [x] Enhanced execution flow in estimation and task views
- [x] Updated `Execute.swift` with improved process handling

---

### 📦 Dependencies & Project Structure

- [x] Updated `Package.resolved` and RsyncUIDeepLinks package revision
- [x] Updated Makefile configuration
- [x] Updated `project.pbxproj` with structural changes
- [x] Added version 2.8.1 JSON configuration files
- [x] Updated README.md and Sonoma JSON to reference v2.8.0

---

### 🧹 Code Quality Improvements

- [x] Consistent code formatting improvements across multiple files
- [x] Enhanced `ReadAllTasks` utility with better error management
- [x] Improved alert handling patterns in views
- [x] Refactored `ActorReadSynchronizeConfigurationJSON` for better readability
- [x] Updated `EditValueErrorScheme` with refined error handling

---

### Key Files Modified
- EstimateExecute (split into Estimate.swift and Execute.swift)
- Logging.swift
- RemoteDataNumbers.swift
- SynchronizeProgressView.swift (extracted)
- RestoreTableView.swift
- Multiple view files in Views

---

### Testing Focus
- Verify estimation and execution separation works correctly
- Test error handling for missing stats and log records
- Validate progress tracking in restore operations
- Confirm all removed features (network monitoring, verify widgets) don't cause issues

---

**Release Target:** v2.8.1rc1  
**Branch:** version-2.8.1  
**Previous Release:** v2.8.0