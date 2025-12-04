+++
author = "Thomas Evensen"
title = "Version 2.7.8"
date = "2025-11-19"
tags = ["changelog","version 2.7.8"]
categories = ["changelog"]
+++

### Version 2.7.8 (build 169) - Nov 19, 2025

There have been updates to the Swift Packages, and the logging section has been cleaned up and several unnecessary log statements have been removed. Additionally, the release build does not contain any log statements, and the make procedure (building a new release) omits all logger DEBUG statements.

The refactor has been completed. The next release version, 2.7.9, is scheduled for release in December. However, additional testing is required to ensure the reliability of the refactored RsyncArguments. All SPMs now have dedicated tests for each. 

### Logger

Within RsyncUI, I utilize Swift Logger to display in Xcode Console whether a call is on the main thread or a background thread. Upon reviewing the logging, I discovered an excessive number of log statements. Consequently, logging statements are disabled for the release build, but they are enabled (by DEBUG flag) when running RsyncUI in Xcode only.

I have removed numerous "boilerplate code" for log statements and instead enhanced the Logger (by extension Logger) with new functions. Replacing all logging statements in code applies to numerous files. 

### Real-Time Output

Real-time output from rsync is now included. You can find it within the "hidden" menu, accessible using the shortcut `⌘S` to reveal concealed toolbar options. The real-time view captures all output from rsync as it happens. The capture requires some additional CPU when activated, and it is automatically enabled and disabled when opening and closing the view. Additionally, the captured output is stored in memory and is cleared when the view is closed or by using the Clear button.

The real-time output captures the rsync output by an actor without blocking the @MainActor and UI updates. However, the @Observable object monitoring updates is executed on the @MainActor and updates the real-time view.

### Schedules

A bug related to deleting schedules has been fixed, and upon request, the weekly schedule has been reinstated. Schedules can only be added for the current and the next month. This restriction is implemented to manage memory usage effectively, as every schedule includes the callback action, which is stored in memory. Schedules are automatically saved to a file and reloaded into memory upon startup.

### Charts

A bug in the charts has been fixed. The bug could cause RsyncUI to crash.

### Concealing Distractions

By using the shortcut `⌘S` (for showing or hiding) or by accessing the Task main menu, the Charts and Quick task will be displayed. They are concealed by default. To reveal them, simply toggle the show or hide option using the shortcut.
