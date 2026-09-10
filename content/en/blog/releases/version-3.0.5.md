+++
author = "Thomas Evensen"
title = "Version 3.0.5"
date = "2026-09-10"
tags = ["changelog","version 3.0.5"]
categories = ["changelog"]
+++

#  RsyncUI 3.0.5 — Changelog

<div class="alert alert-secondary" role="alert">

This build is the latest release; it addresses a crash occurring during compilation and execution of RsyncUI on macOS 27 beta releases. The issue manifested when selecting Tasks from the sidebar menu. The latest build also includes restore, snapshot deletion, synchronization, logging, and shared widget storage fixes completed after the first 3.0.5 tag.

Build by Xcode 27 RC1 on macOS 27 RC (macOS Golden Gate).

</div>

Changes since `v3.0.3` through commit `b3e9343` (September 10, 2026).

A general issue with delete arose from a missing focus state tied to a Swift update, which was resolved in the August 13 build. Additional fixes through September 7 stabilize restore workflows, process completion handling, snapshot deletion, and shared JSON storage used by the widget.

## 🐛 Fxes

- Fixed the recurring AppKit `Update Constraints in Window` crash during startup.
- Replaced the problematic root `NavigationSplitView` implementation.
- Stabilized task-menu identities and selection handling.
- Removed an invisible task editor that caused unnecessary Inspector layout updates.
- Moved Add Task presentation into a dedicated sheet.
- Added stable Inspector presentation state and column sizing.
- Fixed a bug in deep links (URL), now executing the command from a terminal `open "rsyncuiapp://loadprofileandestimate?profile=AnyProfile"` will open RsyncUI and execute estimate & execute for profile `AnyProfile`

## 🎨 Interface improvements

- Redesigned the sidebar as a fixed-width, 220-point panel with a flexible detail area.
- Added a dedicated toolbar button for showing and hiding the sidebar.
- Organized sidebar entries into Actions, Tools, and Management sections.
- Preserved context-sensitive Snapshot and Restore entries.
- Retained profile selection, scheduling status, version information, and notification messages.
- Removed unwanted outer padding from the main application interface while retaining padding on the startup screen.

## ▶️ Synchronization details

- Anchored the Synchronize play button directly to the divider between the two results tables.
- The play button now remains centered between the tables when the window is resized.
- Consolidated synchronization execution and confirmation handling.
- Preserved process ownership while canceling remaining batch tasks.
- Recorded backup success only after a successful process exit.
- Fixed synchronization countdown behavior.

## ♻️ Restore and snapshot fixes

- Preserved the complete restore file list while searching.
- Reset restore snapshot selection when the selected profile or restore context changes.
- Validated restore operations against the currently displayed destination.
- Fixed snapshot deletion path validation and shell quoting.
- Added restore destination, restore search, restore selection, and snapshot deletion regression tests.

## 🧾 Logging and storage

- Fixed Swift concurrency issues in log storage.
- Updated shared JSON storage used by RsyncUI and the widget for build 207.
- Kept profile creation errors visible until the underlying issue is resolved.

## 📦 Version and update information

- Updated the application version from `3.0.3` to `3.0.5`.
- Updated the application and widget build number from `201` to `208`.
- Updated the version feed so supported older releases point to the `v3.0.3` download.
- Added `3.0.2` to the supported update-feed entries.
- Updated README release information and download badges for `v3.0.3`.

## 🧹 Repository maintenance

- Removed obsolete repository instruction files.
- Removed the old `changestr.md` changelog file.
- Simplified project documentation.

## ✅ Verification

- Application builds successfully with Swift 6.
- All 70 tests across 16 suites pass.
- Startup was verified using existing profiles, configurations, and schedules without triggering the previous layout crash.
