+++
author = "Thomas Evensen"
title = "Version 2.9.2"
date = "2026-03-05"
tags = ["changelog","version 2.9.2"]
categories = ["changelog"]
+++

### Version 2.9.2 - March 5, 2026 - development build

<div class="alert alert-danger" role="alert">

Thanks to GitHub user [Tim Reichen](https://github.com/timreichen) for valuable input and suggestions for updates in this release. 

</div>

## Detailed Code Changes: v2.9.1 → 2.9.2dev1

**Summary:**
- Major refactor of Inspector views: new tabbed interface, modular SwiftUI views.
- File moves, renames, and deletions for better organization.
- Updates to documentation, project, and build files.
- Minor business logic and observable state changes.

---

### Key File Changes

- **InspectorViews Refactor:**
  - `DefaultView.swift` **deleted**
  - **New:** `EditTabView.swift` (main inspector tab view)
  - **New:** `LogRecordsTabView.swift` (moved/renamed from `LogsbyConfigurationView.swift`)
  - **New:** `VerifyTaskTabView.swift` (moved/renamed from `VerifyTasks.swift`)
  - Several files renamed/moved for clarity (e.g., `RsyncCommandView.swift`, `VerifyTaskTabView.swift`)

- **Tabbed Inspector UI:**
  - `EditTabView` introduces a tabbed inspector: Edit, Parameters, Log Records, Verify Task
  - Each tab is a separate SwiftUI view

- **Log Records & Verification:**
  - Dedicated inspector tabs for log records and verify task
  - Improved state management and SwiftUI integration

- **Observable State Updates:**
  - Minor changes in `ObservableAddConfigurations.swift`, `ObservableParametersRsync.swift`

- **Project/Build Files:**
  - `RsyncUI.xcodeproj/project.pbxproj`, `Makefile`, `versionRsyncUI.json` updated

- **Documentation:**
  - `README.md`, `QUALITY_ANALYSIS_DETAILED.md` updated

---

### File Change Table

| File/Folder                                               | Change Type   | Description/Notes                                 |
|-----------------------------------------------------------|--------------|---------------------------------------------------|
| RsyncUI/Views/InspectorViews/DefaultView.swift            | Deleted      | Old inspector view removed                        |
| RsyncUI/Views/InspectorViews/EditTabView.swift            | Added        | New main inspector tab view                       |
| RsyncUI/Views/InspectorViews/LogRecords/LogRecordsTabView.swift | Added/Move | Log records inspector tab (was LogsbyConfigurationView) |
| RsyncUI/Views/InspectorViews/VerifyTask/VerifyTaskTabView.swift | Added/Move | Verify task inspector tab (was VerifyTasks.swift)  |
| RsyncUI/Views/InspectorViews/RsyncParameters/extensionRsyncParametersView.swift | Deleted | Refactored into new tabbed structure              |
| RsyncUI/Model/Global/ObservableAddConfigurations.swift    | Modified     | State changes for new inspector                   |
| RsyncUI/Model/Global/ObservableParametersRsync.swift      | Modified     | State changes for new inspector                   |
| RsyncUI.xcodeproj/project.pbxproj                         | Modified     | Project file updates for new/removed files        |
| Makefile, versionRsyncUI.json                             | Modified     | Version/build updates                             |
| README.md, QUALITY_ANALYSIS_DETAILED.md                   | Modified     | Documentation and quality analysis updates        |

---

### Quality & Architecture

- Refactor improves modularity, maintainability, and user experience in Inspector area.
- New tabbed inspector is more extensible for future features.
- Documentation and quality analysis updated to match new codebase state.

---

*For a file-by-file or code-diff summary, ask for a specific file or feature.*

