+++
author = "Thomas Evensen"
title = "Version 3.5.0 — Remove Scheduling"
date = "2026-10-30"
tags = ["changelog","version 3.5.0","scheduling"]
categories = ["changelog"]
+++

# RsyncUI 3.5.0 — Planned release

> **Built-in alternative for scheduling:** On macOS Tahoe 26 or later, you can use Apple Shortcuts to schedule RsyncUI directly, without ScheduleRsync. See [Schedule with Apple Shortcuts](#schedule-with-apple-shortcuts) at the end of this changelog.

<div class="alert alert-info" role="alert">

Version 3.5.0 will be the next release in a few weeks. Its main objective is the removal of scheduling code in RsyncUI. There is a new separate application, **ScheduleRsync**, which keeps track of when profiles should run, while RsyncUI will continue to estimate and synchronize their tasks. Version 3.5.0 also includes localization for Simplified Chinese introduced in the version-3.2.0 pre-release. 

See below about more details about how to trigger RsyncUI external by URL.

Versions 3.1.0 and 3.2.0 of RsyncUI support external URL commands but require a manual restart of RsyncUI to apply new ones. Version 3.5.0 automatically closes after each external URL command completes.

</div>

You can use any scheduling tool to schedule backups with RsyncUI, provided it can run a command that macOS understands, such as from a terminal view:

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

## Schedule with Apple Shortcuts

**Apple Shortcuts is a straightforward alternative to ScheduleRsync for simple daily or weekly schedules.** It is included with macOS. Time-based automations require macOS Tahoe 26 or later; older macOS versions can run shortcuts manually but do not offer this built-in time trigger.

### Create the shortcut

1. Open **Shortcuts** on your Mac and create a new shortcut, for example **RsyncUI — Default**.
2. Add the **URL** action and enter:

   ```text
   rsyncuiapp://loadprofileandestimate?profile=Default
   ```

3. Add **Open URLs** after the URL action, using the URL from the previous action as its input.
4. Replace `Default` with the required RsyncUI profile name. URL-encode special characters in the profile name, for example `My%20Backup` for `My Backup`.
5. Run the shortcut manually once to check that RsyncUI opens with the correct profile, and approve any macOS permission prompt. **This test can start synchronization**, so use a profile that is ready to run.

### Schedule the shortcut

1. In Shortcuts, open **Automation** and add a new automation.
2. Select **Time of Day**, choose the start time, and select the required daily, weekly, or monthly recurrence.
3. Choose the shortcut you created. Select **Run Immediately** so it runs without waiting for confirmation; wording and placement can vary with the macOS version.
4. Create additional shortcuts or time automations for other profiles and start times as needed.

RsyncUI must be installed and registered for the `rsyncuiapp` URL scheme. Keep the Mac awake and the user logged in for the scheduled run; this setup does not configure the Mac to wake. Shortcuts sends the same URL command as ScheduleRsync, so RsyncUI remains responsible for estimation and synchronization.

This alternative does not read ScheduleRsync's schedule file or automatically apply its quiet hours, global minimum gap, adjusted/skipped-run planning, or wake catch-up rules. Choose times outside your quiet hours and leave enough time between profiles for synchronization to finish. Disable equivalent schedules in other tools to avoid duplicate starts.

For background and setup information, see Apple's [Shortcuts User Guide for Mac](https://support.apple.com/guide/shortcuts-mac/welcome/mac) and [macOS Tahoe feature overview](https://www.apple.com/nz/os/pdf/All_New_Features_macOS_Tahoe_Sept_2025_NZ_Final.pdf).

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


