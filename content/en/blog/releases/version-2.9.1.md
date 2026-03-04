+++
author = "Thomas Evensen"
title = "Version 2.9.1"
date = "2026-03-04"
tags = ["changelog","version 2.9.0"]
categories = ["changelog"]
+++

### Version 2.9.1 - March 4, 2026

<div class="alert alert-danger" role="alert">

Thanks to GitHub user [Tim Reichen](https://github.com/timreichen) for valuable input and suggestions for updates in this release. 

</div>

## 🗑️ Removed Features

- **Removed "Two Tables Inspector" option** — the `usetwotablesInspector` setting and the entire `InspectorViewstwotables` view hierarchy (~750 lines) have been deleted, consolidating to a single Inspector layout
- **Removed manual "Save" buttons** from all Settings views (Log, SSH, Environment, Rsync & Path) — settings now **auto-save** on change

## 💾 Auto-Save Settings

- All settings (log options, SSH config, environment variables, rsync paths, restore paths, mark days) now automatically persist when modified via `onChange` handlers

## 🎨 UI Improvements

- Default backup ID label changed from `"Synchronize ID"` → `"No ID set"` for clarity
- Tasks without a `--delete` parameter now display in **blue** text (previously unstyled)
- Added `"No task selected"` placeholder text when no task is selected in Edit/Parameters views
- Simplified the **HelpView** — removed `add` and `deleteparameterpresent` parameters; streamlined to show text + close button
- Improved help text wording for `--delete` parameter guidance (now references Documentation)
- Toolbar "+" button placement changed to `.status`
- Removed extra `Spacer()` toolbar items

## 🔧 Code Quality & Cleanup

- Converted `//` comments to `///` doc-comments across ~100+ locations
- Expanded single-line computed properties to multi-line format (SwiftLint compliance)
- Removed redundant `Sendable` conformance from `AttachedVolumesService`, `TCPconnections`, `SharedConstants`
- Removed custom `==` implementations from `SchedulesConfigurations` and `Log` (using synthesized conformance)
- Eliminated unnecessary intermediate variables (direct `return` statements)
- Removed `self.` prefix where unnecessary (`self.port` → `port`)
- Deleted unused build scripts (`VSC/setup-build-dirs-*.sh`)

## 🔧 DetailsView Enhancement

- Output row view now conditionally renders `RsyncOutputRowView` (rsync v3) vs `OpenRsyncOutputRowView` (open rsync) based on rsync version

## 📦 Dependencies

- Updated **RsyncAnalyse** package to latest revision
- Widget marketing version aligned to `2.9.1` (was stuck at `2.8.0`)

## 🧪 Tests

- Removed unnecessary `async` from test functions that don't need it
- Simplified `@Suite` attributes (removed redundant name strings)

## 📄 Documentation

- Updated **README.md** with cleaner structure (sections for Requirements, Installation, Version, Documentation)
- Updated **QUALITY_ANALYSIS_DETAILED.md** to v2.0 with current metrics