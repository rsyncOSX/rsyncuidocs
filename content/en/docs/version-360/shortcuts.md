+++
author = "Thomas Evensen"
title = "Shortcuts, Siri and Spotlight"
linkTitle = "4. Shortcuts"
date = "2026-11-26"
weight = 40
description = "Create and run a Synchronize Tasks shortcut in the Shortcuts app."
tags = ["version 4.0.0"]
categories = ["version 4.0.0"]
+++

RsyncUI adds two actions to the Shortcuts app. They also work from Siri and Spotlight, without opening the RsyncUI window, and RsyncUI quits by itself when the action is done.

<div class="alert alert-info" role="alert">

**"Unknown Action" in Shortcuts?** If a shortcut shows *Unknown Action* and stops with *The operation couldn't be completed. (WFActionErrorDomain error 1.)*, Shortcuts cannot load the RsyncUI action from macOS. There are two known causes.

**1. The macOS App Intents service has lost its database.** The service *linkd* keeps the actions of all apps in a database. If that database is gone, Shortcuts lists the RsyncUI actions but cannot load them. This is a macOS problem, and it can affect actions from other apps too. Restart the services in Terminal. macOS starts them again by itself:
```bash
killall linkd siriactionsd
```
The message *No matching processes belonging to you were found* only means one of the services was not running, and can be ignored. If this does not help, log out and back in, or restart the Mac.

**2. macOS has matched the action to another copy of RsyncUI.** This can be an older version, a mounted RsyncUI disk image or an Xcode build. Eject all mounted RsyncUI disk images, delete or move away other copies of RsyncUI.app, and keep the copy in */Applications*. Then register it again:
```bash
/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -f -R /Applications/RsyncUI.app
```

**After either fix:** quit Shortcuts, open RsyncUI from */Applications* once and quit it. In the shortcut, delete the *Unknown Action* step with the ✕ and add **Synchronize Tasks** (or **Estimate Tasks**) again. A step that is already in a shortcut is not repaired automatically.

To see which copies of RsyncUI macOS knows about:
```bash
/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -dump | grep -E "^path:.*RsyncUI\.app \("
```
A copy you cannot delete can be unregistered with `lsregister -u "<path to RsyncUI.app>"`.

</div>

| Action | What it does |
| --- | --- |
| **Estimate Tasks** | A dry run of a profile, or of selected tasks. Reports files to transfer, size and files to delete. Changes nothing, and works for every task. |
| **Synchronize Tasks** | Estimates first, then synchronizes the tasks that have changes, following each task's own `--delete` setting. Writes log records like a run in RsyncUI. |

*Synchronize Tasks* only runs tasks that are allowed in Shortcuts (see *Verify and allow a task*). Before synchronizing, it also stops when:

- the source folder of a task with `--delete` is missing or empty, for example a disconnected drive
- **Confirm execute** is turned on in Settings and the estimate needs confirmation
- the estimate shows more deletions than the optional **Maximum Deletions** in the shortcut
- RsyncUI is already running a task

The actions, messages and Siri phrases are available in English, Simplified Chinese and Traditional Chinese. Example Siri phrases: *"Estimate Documents in RsyncUI"* and *"Synchronize Documents with RsyncUI"*, where *Documents* is a profile name.

## RsyncUI actions in Shortcuts

{{< figure src="/images/version400/nr9.png" alt="RsyncUI actions in the Shortcuts app" position="center" style="border-radius: 8px;" >}}

In the Shortcuts app, search for *rsyncui* to find the two RsyncUI actions: **Estimate Tasks** and **Synchronize Tasks**.

## Create a Synchronize Tasks shortcut

{{< figure src="/images/version400/nr10.png" alt="Synchronize Tasks action" position="center" style="border-radius: 8px;" >}}

Adding **Synchronize Tasks** creates the action *Synchronize Tasks in Default*. Choose the profile, and optionally the tasks (leave empty for all tasks in the profile). The expand arrow shows more options, such as **Maximum Deletions**.

## The shortcut in the library

{{< figure src="/images/version400/nr11.png" alt="Shortcut in the Shortcuts library" position="center" style="border-radius: 8px;" >}}

The new shortcut appears under *All Shortcuts* and can be run from the Shortcuts app, Siri or Spotlight.

## Tasks not allowed

{{< figure src="/images/version400/nr12.png" alt="Not allowed in Shortcuts message" position="center" style="border-radius: 8px;" >}}

Running the shortcut while only *GitHub backup* is allowed stops with a message listing the tasks that are not allowed (*GitDocuments* and *DXO Database V9*), asking you to verify them in RsyncUI and allow them in Shortcuts.

## All tasks allowed

{{< figure src="/images/version400/nr13.png" alt="All tasks allowed" position="center" style="border-radius: 8px;" >}}

After verifying and allowing the remaining tasks, every task in the list has a green checkmark. With no task selected, the inspector says *Select a task*.
