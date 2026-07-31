+++
author = "Thomas Evensen"
title = "Version 3.0.3"
date = "2026-07-31"
tags = ["changelog","version 3.0.3"]
categories = ["changelog"]
+++

# 🚀 Changelog: RsyncUI 3.0.2 → 3.0.3 

Thanks to [Tim Reichen](https://github.com/timreichen) for submitting PRs to this release. If no bugs are reported by next week, this commit will become the next official release without requiring a new build. Consequently, users who download and test it now will not receive a notification to download a new version later.

# 📦 RsyncUI 3.0.3

Changes since **v3.0.2**, through commit `6dd6322f` on July 29, 2026.

## ✨ Improvements

- Redesigned the Add Task interface using a cleaner grouped form layout.
- Added a simpler toggle for controlling the trailing slash on source folders.
- Unified the first-task experience with the standard Add Task sheet.
- Added standard confirmation and cancellation buttons to the Add Task and Add Profile sheets.
- Updated Add Task and Add Profile toolbar controls to compact icon buttons.
- Improved the About window’s Close button and toolbar integration.
- Improved labels, field descriptions, validation borders, and browse buttons.
- Hidden the redundant inspector tab label.
- Marked delete confirmation actions as destructive for tasks, schedules, and snapshots.
- Simplified saving URLs for the RsyncUI widget.

## 🛠️ Fixes

- Fixed trailing-slash handling when adding and editing tasks.
- Fixed trailing-slash handling for Quick Tasks, including migration of existing preferences.
- Preserved exact configured paths instead of rewriting them during configuration validation.
- Fixed the selected task type not being refreshed when switching configurations.
- Fixed rsync itemized-output parsing for filenames containing leading spaces.
- Fixed parsing of deleted items for different rsync versions.
- Fixed placement of `--itemize-changes` when rsync arguments contain the `--` option terminator.
- Fixed estimation and execution states not completing correctly after process errors.

## 🎨 Interface Changes

- Profiles without tasks now automatically open the shared Add Task sheet.
- Task fields now use standard SwiftUI controls and grouped sections.
- The task action selector now uses a menu-style picker.
- The trailing-slash selector is now an on/off toggle focused specifically on the source folder.
- The dedicated first-task view and duplicated Add Task helper views were removed.

## ⚡ Quick Tasks

- Simplified the trailing-slash preference to a Boolean toggle.
- Added compatibility migration for the previous trailing-slash preference format.
- Trailing slashes are now applied only to the Quick Task source path.
- Added safeguards against duplicate trailing slashes.
- Added handling to preserve the filesystem root path correctly.

## 🧪 Reliability

- Added tests for itemized rsync output parsing.
- Added tests for configuration selection and task-type updates.
- Added tests for Quick Task source-path handling.
- Updated configuration validation tests for the new trailing-slash behavior.

## 🔧 Technical Changes

- Updated the application and widget marketing version to **3.0.3**.
- Updated the build number from **196** to **201**.
- Updated project targets to Swift 6.
- Updated `ParseRsyncOutput` to version **1.0.1**.
- Removed the unused `RsyncAnalyse` package dependency.
- Updated release metadata and download links for newer RsyncUI versions.
