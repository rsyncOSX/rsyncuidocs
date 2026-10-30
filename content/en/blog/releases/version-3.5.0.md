+++
author = "Thomas Evensen"
title = "Version 3.5.0 — Planned scheduling changes"
date = "2026-10-30"
tags = ["changelog","version 3.5.0","scheduling"]
categories = ["changelog"]
+++

# RsyncUI 3.5.0 — Planned release

*Versions 3.1.0 and 3.2.0 support external URL commands but require a manual restart of RsyncUI to apply new ones. Version 3.5.0 automatically close after each external URL command completes.*

You can use any scheduling tool to schedule backups with RsyncUI, provided it can run a command that macOS understands, such as:

```sh
open "rsyncuiapp://loadprofileandestimate?profile=Default"
```

This opens RsyncUI, loads the selected profile, estimates its tasks, and automatically starts synchronization. Replace `Default` with your profile name, URL-encoding it when necessary. RsyncUI must be installed, and the Mac must be awake when the scheduling tool runs the command. ScheduleRsync provides a dedicated interface for managing these schedules, but you can choose another tool that supports running this command.

In a macOS Swift application, use AppKit to open the same URL:

```swift
import AppKit

@MainActor
func triggerRsyncUI(profile: String = "Default") {
    var components = URLComponents()
    components.scheme = "rsyncuiapp"
    components.host = "loadprofileandestimate"
    components.queryItems = [URLQueryItem(name: "profile", value: profile)]

    guard let url = components.url else { return }
    if !NSWorkspace.shared.open(url) {
        print("Unable to open RsyncUI.")
    }
}
```

`URLComponents` encodes the profile name for the URL. Call `triggerRsyncUI(profile: "Default")` on the main actor when the schedule is due. Opening the URL hands the command to RsyncUI; it does not confirm that synchronization has completed.

<div class="alert alert-info" role="alert">

Version 3.5.0 is a future release. Its main objective is to move scheduling out of RsyncUI and into a separate application, **ScheduleRsync**. ScheduleRsync will keep track of when profiles should run, while RsyncUI will continue to estimate and synchronize their tasks.

**There are no compiled versions available to test yet.** If you need a proper scheduling function and would like to help test it, please [open an issue in the RsyncUI repository](https://github.com/rsyncOSX/RsyncUI/issues). Compiled versions will then be made available for testing.

</div>

## Scheduling in ScheduleRsync

The built-in scheduling function is removed from RsyncUI in version 3.5.0 in test. Use ScheduleRsync to select an RsyncUI profile, choose its first run date and time, and create a schedule:

- **Once:** run at the selected date and time.
- **Daily:** repeat each day.
- **Weekly:** repeat each week.
- **Repeat:** run at a fixed interval in whole minutes, with a minimum of 30 minutes.

ScheduleRsync shows upcoming runs in a calendar and schedule list. You can inspect the profiles and times for a day, or delete a schedule series to remove its future runs.

{{< figure src="/images/newschedule/newschedule.png" alt="ScheduleRsync calendar and scheduling controls" position="center" style="border-radius: 8px;" >}}

### Spacing and quiet hours

A global **Minimum between tasks** setting spaces scheduled starts across all profiles. The default is 15 minutes. This is a gap between start times; ScheduleRsync does not receive a completion notification from RsyncUI.

An optional **Quiet period**, enabled by default from 23:00 to 07:00 local time, moves starts out of those hours. Conflicting starts are delayed while keeping the original recurrence. If a delayed run would reach the next occurrence in its series, or fall outside the planning horizon, it is skipped. Adjusted runs are shown in yellow and skipped runs in red.

### Keep ScheduleRsync running

ScheduleRsync must remain running with its main window open. Closing that window quits the app and stops scheduling. It does not install a background service or wake the Mac, so keep the Mac awake for runs to start on time.

After the Mac wakes, ScheduleRsync catches up on overdue runs. Multiple missed repeats are combined into one catch-up run per schedule, subject to spacing and quiet hours. Runs missed while ScheduleRsync was closed are skipped when it next opens.

### Existing schedules

ScheduleRsync uses the existing RsyncUI schedule file, `~/.rsyncosx/<Mac serial>/schedule.json`, and reads profiles from the same configuration directory. Existing once, daily, and weekly schedules remain readable without copying or migrating the file. Avoid running the scheduler in an older RsyncUI version alongside ScheduleRsync, as both applications could trigger the same schedules.

## How ScheduleRsync triggers RsyncUI

When a schedule becomes due, the planned integration opens RsyncUI using its external URL command. For the Default profile, the command is:

```text
rsyncuiapp://loadprofileandestimate?profile=Default
```

ScheduleRsync substitutes the selected profile name and URL-encodes it. macOS delivers the URL to RsyncUI, launching the application if needed. RsyncUI loads that profile, estimates its tasks, and automatically starts synchronization. RsyncUI must be installed and registered to handle the `rsyncuiapp` URL scheme. See [URL commands]({{< relref "/docs/advanced/url-commands.md" >}}) for more details.

ScheduleRsync manages the timing; RsyncUI performs the actual synchronization. RsyncUI may reject an incoming command if another operation is already in progress, so allow enough time between scheduled starts for your profiles to finish.
