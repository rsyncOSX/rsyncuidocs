+++
author = "Thomas Evensen"
title = "Version 2.9.2"
date = "2026-03-11"
tags = ["changelog","version 2.9.2"]
categories = ["changelog"]
+++

### Version 2.9.2 - March 11, 2026 

<div class="alert alert-danger" role="alert">

Thanks to GitHub user [Tim Reichen](https://github.com/timreichen) for valuable input and suggestions for updates in this release. 

</div>

## Detailed Code Changes: v2.9.1 → 2.9.2

There are no changes to the model, only UI-updates. All details about a task is now moved to the Tasks menu. Cleaned up the Sidebar. There is a link to info about the `--delete` parameter. 

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

### Quality & Architecture

- Refactor improves modularity, maintainability, and user experience in Inspector area.
- New tabbed inspector is more extensible for future features.
- Documentation and quality analysis updated to match new codebase state.

---

{{< figure src="/images/v292/first.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v292/edit.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v292/parameters.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v292/logs.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v292/verify.png" alt="" position="center" style="border-radius: 8px;" >}}


