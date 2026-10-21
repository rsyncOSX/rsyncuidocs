+++
author = "Thomas Evensen"
title = "Version 3.1.0"
date = "2026-10-21"
tags = ["changelog","version 3.1.0"]
categories = ["changelog"]
+++

# RsyncUI 3.1.0 — Changelog

<div class="alert alert-secondary" role="alert">

Version 3.1.0 improves the Synchronize view and task creation, fixes profile sorting, and includes the rsync error-reporting fixes introduced in the 3.0.6 release candidate.

If no issues are discovered in the release candidate, it will be published as the stable 3.1.0 release using the same builds; no new builds will be produced.

</div>

Changes since `v3.0.5` through commit `9d3903a4` (October 21, 2026).

## 🎨 Synchronize view improvements

- Added a heading showing the current profile, task count, and selection count.
- Added a details panel for a single selected task, showing its source and destination hosts and full, selectable folder paths. The panel adapts to the available width.
- Corrected source and destination display for remote-pull tasks, including halted tasks that retain their remote-pull mode.
- Simplified the task table with clearer Task and Last run headings, destination host and folder details, and tooltips for truncated paths.
- Added clearer Halted and Never run indicators and adjusted status colors.
- Added selection guidance explaining when actions apply to all enabled tasks and when to estimate selected tasks.
- Kept Estimate & Sync visible but disabled when all tasks are halted.

## ➕ Task creation improvements

- Replaced red field borders with Required markers and contextual guidance for missing folders, remote users, and remote servers.
- Clarified source and destination labels for remote-pull tasks.
- Disabled Add until required fields are complete and added a matching check before attempting to create a task.
- Added guidance for completing remote connection fields or clearing them for a local task.

## 🐛 Error reporting and profile fixes

- Fixed rsync output error checking so it follows the user's configured preference instead of always being enabled.
- Improved failure alerts to include the rsync exit code and a concise summary of standard error output.
- Limited the output shown in failure alerts to ten lines, preserving the most recent line containing “error” when it would otherwise fall outside the displayed summary.
- Fixed profile-name sorting on APFS filesystems using localized natural ordering. Newly created profiles are also inserted in sorted order.

## 🧪 Regression coverage

- Added tests for large multiline error output, error messages across multiple output chunks, and short or empty output.
- Added tests for failure-alert presentation and for enabling or disabling rsync output error checking.

## 🙏 Thanks

- Thanks to [@daLuiz](https://github.com/daLuiz) for reporting [the rsync error-reporting issue](https://github.com/rsyncOSX/RsyncUI/issues/183).
- Thanks to [@jigawho-ship-it](https://github.com/jigawho-ship-it) for reporting the profile-name sorting issue on APFS filesystems.

## 📦 Version information

- Updated the application and widget version to `3.1.0`.
- Updated the application and widget build number from `208` to `210`.
