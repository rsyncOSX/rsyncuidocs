+++
author = "Thomas Evensen"
title = "Version 3.0.2"
date = "2026-06-24"
tags = ["changelog","version 3.0.2"]
categories = ["changelog"]
+++

# 🚀 Changelog: RsyncUI 3.0.0 → 3.0.2 (release candidate)

Based on the actual Git diff from v3.0.0 to commit 64a97b8a dated June 24, 2026.

## 📋 Improved rsync output

- Added structured presentation of itemized rsync output.
- Changes are classified as added, updated, deleted, metadata-only, or other.
- Added colored icons and clearer file paths for each change.
- Added support for both rsync and openrsync output formats.
- Automatically enables --itemize-changes during synchronization, estimation, and verification.
- Ensures the option is added only once and does not modify saved task parameters.

## 🗓️ More reliable scheduling

- Fixed duplicate daily and weekly schedules after recomputation or application restart.
- Improved persistence by storing schedule definitions instead of generated occurrences.
- Fixed schedule calculation across month and year boundaries.
- Schedules are now limited correctly through the end of the following month.
- Invalid, expired, and out-of-range dates are rejected.
- Prevented duplicate schedule definitions.
- Deleting the earliest schedule now correctly activates the next one.
- Deleting the final schedule clears the timer and next-schedule state.
- Improved handling and deletion of schedules missed while the Mac was asleep.
- Schedule selections are cleared after deletion.

## 🧹 Interface improvements

- Removed the redundant reset-selection toolbar button from the log-record view.
- Simplified itemized-output detection.
- Corrected the schedule-type picker value binding.
- Minor cleanup of the log statistics chart implementation.

## ✅ Testing

- Added scheduler tests covering deletion, deduplication, persistence, date validation, and year boundaries.
- Added tests for itemized rsync output parsing.
- Added tests ensuring --itemize-changes is inserted correctly and only once.
- Added a dedicated schedule test tag.

## 🔧 Maintenance

- Updated the application and widget version to 3.0.2 (build 196).
- Updated release and download references for the 3.0 series.
- Updated development documentation.
- Diff summary: 25 files changed, 591 insertions, and 229 deletions.

{{< figure src="/images/ver302/output.png" alt="" position="center" style="border-radius: 8px;" >}}

