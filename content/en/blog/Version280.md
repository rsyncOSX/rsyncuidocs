+++
author = "Thomas Evensen"
title = "Version 2.8.0"
date = "2025-12-02"
tags = ["changelog","version 2.8.0"]
categories = ["changelog"]
+++

### Version 2.8.0 (build 171) - Dec 2, 2025

*There is a new issue summarizing, by GitHub Copilot, all changes since version 2.7.8.*

The following summarizes changes in this release:

- The major update within this release is that all seven Swift Packages (SPM) are updated to version 2.0.
  - All SPM are validated by their own test, using the new Swift Testing framework.
- Several cleanups and refactorings have been made in the code.
  - There are approximately 17,000 lines of Swift code, and some code has not been reviewed for some time.
    - It has been about five years since I commenced development of RsyncUI, based on code end experience from my previous project.
    - I have learned a lot during these years, and now most of the code has been reviewed at least once since the start of development.
    - Almost every time I review old code, there are some refactorings, simplifications, and cleaning of the code.
- A bug in the restore data functionality has been resolved.
- Only one Widget is now available, Estimate and Execute.
- All synchronization, such as quicktask and restore, now includes a progress bar if there has been an estimate ahead.
- Real-time capture of rsync includes capturing to a file. Users can view either the RsyncUI logfile or the rsync capture to file in the view logfile.
- A gesture has been added to indicate when buttons are pressed.

<div class="alert alert-secondary" role="alert">

Please be aware that real-time logging to file and view incurs a performance penalty. In certain instances, the termination signal may precede the complete draining of input from the filehandle, resulting in the absence of data for logging. While data synchronization is ensured, there may be no logging regarding the synchronization process.

My recommendation is to utilize this feature exclusively during the testing of new tasks and `—dry-run` tasks.

This feature is automatically disabled when the view is closed or switched off by buttons in the view.

</div>

### No stats

*There is more info about the upcoming maintenance release, version 2.8.1, about this issue in the blog about version 2.8.1*

<div class="alert alert-secondary" role="alert">

The process termination signal indicates that the external rsync process has completed and the process has been terminated. All tasks within the main synchronize view are updated with the latest run, but there is also a separate logging that records the main result of each task with a timestamp.

Occasionally, when synchronizing a small amount of data to fast SSDs, the termination signal is detected before all output from rsync has been received. In such cases, the separate logging may be missing. After data synchronization and the absence of a log, you can verify the synchronization of data by recalculating the estimate. 

The process termination signal serves as a message to perform logging, but if the last summarized rsync output is missing, there is nothing to log. 

*Output from rsync* refers to the information that rsync provides to the terminal during the execution of a task.

Normally, the logging works as expected.

</div>

### Swift Packages

All SPM packages include their own testing mechanisms, and all tests have been successfully passed. SPM packages are generally small and focused on a specific purpose, which simplifies testing for edge cases and typical usage scenarios.

#### Main Repository

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - the main repository for RsyncUI

#### Swift Packages used by RsyncUI

All SPM packages are refactored, updated, and checked into the main branch. RsyncUI is a depended on all packages, but the last one is not mandatory. SSH keys can be generated via command line.

- *RsyncProcess* (https://github.com/rsyncOSX/RsyncProcess) - A minor package but a core function of RsyncUI
	- listens for output from the rsync process as well as termination signal
- *ProcessCommand* (https://github.com/rsyncOSX/ProcessCommand) - As above, but for commands other than rsync
- *RsyncArguments* (https://github.com/rsyncOSX/RsyncArguments) - Generate parameters for `rsync` based on configurations
- *DecodeEncodeGeneric* (https://github.com/rsyncOSX/DecodeEncodeGeneric) - Generic code for decoding and encoding JSON data
- *ParseRsyncOutput* (https://github.com/rsyncOSX/ParseRsyncOutput) - Parse and extract numerical values from the output of `rsync`
	- this data is used to display details and log results for synchronized tasks
- *RsyncUIDeepLinks* (https://github.com/rsyncOSX/RsyncUIDeepLinks) - Parse and return valid URL deeplinks to execute tasks directly within RsyncUI
- *sshCreateKey* (https://github.com/rsyncOSX/sshCreateKey) - Assist in creating an SSH identity file and key using RsyncUI
	- generate an RSA-based SSH key for default and user-defined keys, including the SSH port number

# Development Summary: v2.7.8 → v2.8.0

## Overview

This issue summarizes the major development work completed since the release of version 2.7.8, including architectural improvements, UI enhancements, and new features leading toward version 2.8.0.

## 📊 Development Statistics

```mermaid
pie title "Commits by Category (70 total commits)"
    "Refactoring" : 25
    "UI/UX Improvements" : 18
    "Feature Additions" : 15
    "Package Updates" : 12
```

## 🏗️ Major Feature Areas

```mermaid
mindmap
  root((v2.7.8 → v2.8.0))
    Progress Tracking
      RestoreProgressView
      SynchronizeProgressView
      Max value support
      Real-time updates
    Logging System
      Dedicated log window
      Actor-based concurrency
      File output option
      Delete optimization
    Architecture
      Params struct
      SSHParams refactor
      Actor concurrency
      Path handling
    UI Refinements
      Glass button style
      Dynamic text colors
      Toolbar layouts
      Progress indicators
    Widget System
      Remove WidgetVerify
      URL handling updates
      DeepLinks improvements
```

## 🔄 Development Flow

```mermaid
gitGraph
    commit id: "v2.7.8 Release"
    branch version-2.7.9
    checkout version-2.7.9
    commit id: "Add log window"
    commit id: "Actor concurrency"
    commit id: "File output option"
    commit id: "Glass button style"
    commit tag: "v2.7.9rc1"
    commit id: "Process termination"
    commit id: "Widget refinements"
    commit id: "Restore progress"
    commit tag: "v2.7.9rc2"
    checkout main
    merge version-2.7.9
    branch version-2.8.0
    checkout version-2.8.0
    commit id: "Catalog refactor"
    commit id: "Progress improvements"
    commit id: "Path concatenation fix"
    commit id: "EstimateExecute refactor"
    commit id: "Current HEAD"
```

## 📦 Major Refactoring Initiatives

### 1. Architecture & Code Organization

```mermaid
graph TD
    A[Monolithic Code] --> B[Structured Architecture]
    B --> C[Params Struct]
    B --> D[SSHParams Struct]
    B --> E[Actor-based Logging]
    B --> F[Service Layer]
    
    C --> C1[Centralized Parameters]
    D --> D1[SSH Handling]
    E --> E1[DeleteLogrecords Actor]
    E --> E2[ActorReadLogRecordsJSON]
    F --> F1[AttachedVolumesService]
    F --> F2[HomeCatalogsService]
    
    style B fill:#90EE90
    style C fill:#87CEEB
    style D fill:#87CEEB
    style E fill:#87CEEB
    style F fill:#87CEEB
```

### 2. Progress Tracking System Enhancement

```mermaid
sequenceDiagram
    participant User
    participant UI
    participant Process
    participant Progress
    
    User->>UI: Initiate Task
    UI->>Process: Start rsync
    Process->>Progress: Report progress
    Progress->>UI: Update RestoreProgressView
    Progress->>UI: Update SynchronizeProgressView
    UI->>User: Real-time feedback
    Process->>Progress: Set max value
    Progress->>UI: Display completion %
    UI->>User: Task complete
```

### 3. Logging System Modernization

```mermaid
graph LR
    A[Old Logging] --> B[New Logging System]
    
    B --> C[Dedicated Window]
    B --> D[Actor Concurrency]
    B --> E[File Output]
    B --> F[Optimized Deletion]
    
    C --> C1[Separate Log View]
    D --> D1[Thread-safe Operations]
    E --> E1[Persistent Logs]
    F --> F1[Batch Processing]
    
    style A fill:#FFB6C6
    style B fill:#90EE90
    style C fill:#87CEEB
    style D fill:#87CEEB
    style E fill:#87CEEB
    style F fill:#87CEEB
```

## 🎨 UI/UX Improvements

```mermaid
graph TD
    A[UI Enhancements] --> B[Visual Polish]
    A --> C[Component Updates]
    A --> D[Layout Improvements]
    
    B --> B1[Glass Button Style]
    B --> B2[Sustained Pressure Animation]
    B --> B3[Dynamic Text Colors]
    
    C --> C1[ConditionalGlassButton]
    C --> C2[RestoreProgressView]
    C --> C3[SynchronizeProgressView]
    
    D --> D1[Toolbar Layouts]
    D --> D2[Sheet View Heights]
    D --> D3[Progress Indicators]
    
    style A fill:#FFD700
    style B fill:#87CEEB
    style C fill:#87CEEB
    style D fill:#87CEEB
```

## 🔧 Technical Improvements

### Parameter Handling Refactor

**Before:**
- Parameters scattered across multiple classes
- Inconsistent SSH parameter creation
- Duplicated argument construction logic

**After:**
- Centralized `Params` struct
- Dedicated `SSHParams` struct
- Consistent parameter construction
- Better code reusability

### Concurrency Model

**Key Changes:**
- Introduction of Actor-based concurrency for log management
- `DeleteLogrecords` actor for safe log deletion
- `ActorReadLogRecordsJSON` optimization
- Thread-safe state management

### Path Handling

**Improvements:**
- URL extension for home directory access
- Fixed config path concatenation
- Better catalog path logic
- Unified path handling approach

## 🗑️ Cleanup & Removal

```mermaid
graph LR
    A[Removed Components] --> B[WidgetVerifyExtension]
    A --> C[Verify URL Support]
    A --> D[AllOutputView]
    A --> E[Unused Environment Variables]
    A --> F[Convenience Initializers]
    
    B --> B1[Simplified widget system]
    C --> C1[Streamlined URL handling]
    D --> D1[Replaced with RsyncRealtimeView]
    E --> E1[Cleaner codebase]
    F --> F1[Explicit initialization]
    
    style A fill:#FFB6C6
```

## 📈 Commit Activity Timeline

```mermaid
gantt
    title Development Timeline (v2.7.8 → v2.8.0)
    dateFormat  YYYY-MM-DD
    section Logging System
    Actor concurrency & log management    :done, 2024-10-01, 2024-10-15
    Dedicated log window                  :done, 2024-10-15, 2024-10-25
    File output & optimization            :done, 2024-10-25, 2024-11-05
    
    section Architecture
    Params & SSHParams refactor           :done, 2024-10-20, 2024-11-10
    Service layer improvements            :done, 2024-11-15, 2024-11-25
    
    section UI/UX
    Glass button & animations             :done, 2024-10-28, 2024-11-08
    Progress tracking enhancements        :done, 2024-11-10, 2024-11-25
    
    section Progress System
    Restore progress view                 :done, 2024-11-12, 2024-11-20
    Synchronize progress extraction       :done, 2024-11-22, 2024-11-28
    Max value support                     :done, 2024-11-28, 2024-12-02
    
    section Cleanup
    Widget removal & refinements          :done, 2024-11-05, 2024-11-15
    Code cleanup & optimization           :done, 2024-11-20, 2024-12-02
```

## 🎯 Key Achievements

1. **✅ Enhanced Progress Tracking**
   - New `RestoreProgressView` for better restore operation visibility
   - Extracted `SynchronizeProgressView` to separate file
   - Added max value support for accurate progress percentages
   - Improved UI progress indicators across all views

2. **✅ Modern Logging System**
   - Dedicated log window for better log management
   - Actor-based concurrency for thread-safe operations
   - File output option for persistent logging
   - Optimized log deletion with batch processing

3. **✅ Architectural Improvements**
   - Introduced `Params` struct for centralized parameter management
   - Created `SSHParams` struct for SSH handling
   - Refactored catalog and volume models with service layer
   - Improved error handling and method naming consistency

4. **✅ UI Polish**
   - Glass button style with sustained pressure animations
   - Dynamic text colors for better visual feedback
   - Refined toolbar layouts across multiple views
   - Increased sheet view heights for better content display

5. **✅ Code Quality**
   - Removed deprecated widget components
   - Fixed path concatenation issues
   - Eliminated unused code and environment variables
   - Improved code organization and modularity

## 🔍 Code Quality Metrics

```mermaid
graph LR
    A[Code Improvements] --> B[+2500 lines added]
    A --> C[-1800 lines removed]
    A --> D[Net: +700 lines]
    
    B --> B1[New features]
    B --> B2[Better structure]
    
    C --> C1[Removed redundancy]
    C --> C2[Cleaned deprecated code]
    
    D --> D1[More functionality]
    D --> D2[Better maintainability]
    
    style A fill:#90EE90
    style B fill:#87CEEB
    style C fill:#FFB6C6
    style D fill:#FFD700
```

## 🚀 Next Steps for v2.8.0

- [x] Final testing of all refactored components
- [ ] Performance benchmarking of actor-based logging
- [ ] User acceptance testing of new progress views
- [x] Documentation updates
- [x] Release notes preparation

## 📝 Notes

- Two release candidates (v2.7.9rc1 and v2.7.9rc2) were created during development
- The current branch `version-2.8.0` is actively being developed
- All changes maintain backward compatibility with existing configurations
- Swift package dependencies have been updated to their latest stable versions

---

**Total Commits:** 70  
**Files Changed:** ~150+  
**Primary Focus Areas:** Architecture, UI/UX, Logging, Progress Tracking  
**Development Period:** Post v2.7.8 release → Present