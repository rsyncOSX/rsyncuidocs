+++
author = "Thomas Evensen"
title = "Version 3.0.4"
date = "2026-08-12"
tags = ["changelog","version 3.0.4"]
categories = ["changelog"]
+++

#  RsyncUI 3.0.4 — Changelog

> This build is not a release candidate; it addresses a crash occurring during compilation and execution of RsyncUI on macOS 27 beta releases. The issue manifested when selecting Tasks from the sidebar menu. Users running macOS 27 beta are advised to update to this version. A new public release of RsyncUI will coincide with the general availability of macOS 27 in the coming weeks.

Changes since `v3.0.3` through commit `5cebb703` (August 12, 2026).

The previous build had some issues with delete profiles, the new build fixes that (commit `cc9fc88 ` on branch version-3.0.4). The build number is `203`.

## 🐛 Crash fixes

- Fixed the recurring AppKit `Update Constraints in Window` crash during startup.
- Replaced the problematic root `NavigationSplitView` implementation.
- Stabilized task-menu identities and selection handling.
- Removed an invisible task editor that caused unnecessary Inspector layout updates.
- Moved Add Task presentation into a dedicated sheet.
- Added stable Inspector presentation state and column sizing.

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

## 📦 Version and update information

- Updated the application version from `3.0.3` to `3.0.4`.
- Updated the application and widget build number from `201` to `202`.
- Updated the version feed so supported older releases point to the `v3.0.3` download.
- Added `3.0.2` to the supported update-feed entries.
- Updated README release information and download badges for `v3.0.3`.

## 🧹 Repository maintenance

- Removed obsolete repository instruction files.
- Removed the old `changestr.md` changelog file.
- Simplified project documentation.

## ✅ Verification

- Application builds successfully with Swift 6.
- All 58 tests across 11 suites pass.
- Startup was verified using existing profiles, configurations, and schedules without triggering the previous layout crash.