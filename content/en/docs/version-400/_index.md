+++
author = "Thomas Evensen"
title = "Version 4.0.0 (test release)"
linkTitle = "Version 4.0.0"
date = "2026-11-26"
weight = 60
description = "What is new in RsyncUI 4.0.0, and a step-by-step walk through the new version."
tags = ["version 4.0.0"]
categories = ["version 4.0.0"]
+++

<div class="alert alert-warning" role="alert">

**This is a test release.** **RsyncUI 4.0.0** is a test version, planned for release in some weeks. It is published in [RsyncUI-next](https://github.com/rsyncOSX/RsyncUI-next/releases) so it can be tested before it is merged into RsyncUI. Please report problems in the [RsyncUI-next issues](https://github.com/rsyncOSX/RsyncUI-next/issues).

</div>

## What is new

### A redesigned interface

- **Synchronize and Tasks workspaces** are rebuilt around the task table, with a persistent preview and run bar, and the synchronization progress shown below the table.
- **A task inspector** for the selected task, with *General*, *Rsync Options*, *Logs* and *Verify* tabs.
- **Clearer task setup**: the task direction and its source and destination are summarised while you create or edit a task.
- **Safer runs**:
  - the run confirmation shows where data goes and which deletion options are in effect
  - a warning when deletion (`--delete`) is enabled
  - confirmation is required when a dry run cannot determine the changes
  - only estimated tasks are synchronized after an incomplete preview
- **Restore, Snapshots and Profiles** follow the same layout as the main workspace.
- **Languages**: Traditional Chinese (zh-Hant) is new, and Simplified Chinese (zh-Hans) is updated for the new interface.

### Shortcuts, Siri and Spotlight

RsyncUI can now be used from the Shortcuts app, Siri and Spotlight, without opening the RsyncUI window. RsyncUI quits by itself when the action is done.

| Action | What it does |
| --- | --- |
| **Estimate Tasks** | A dry run of a profile, or of selected tasks. Reports files to transfer, size and files to delete. Changes nothing, and works for every task. |
| **Synchronize Tasks** | Estimates first, then synchronizes the tasks that have changes, following each task's own `--delete` setting. Writes log records like a run in RsyncUI. |

Tasks must be verified and allowed in RsyncUI before *Synchronize Tasks* runs them. See *Verify and allow a task* and *Shortcuts, Siri and Spotlight* below.

## Before you test

- **Back up your settings.** RsyncUI keeps its tasks, logs and settings in `~/.rsyncosx`. Copy that folder first:
  ```bash
  cp -R ~/.rsyncosx ~/rsyncosx-backup
  ```
- **Going back to 3.5.** Version 3.5 ignores the Shortcuts approvals and drops them if it saves the tasks, so they must be allowed again in 4.0.0. If anything else looks wrong after going back, restore your backup.
- **Homebrew installs the stable version.** To test 4.0.0, download it from the [RsyncUI-next releases](https://github.com/rsyncOSX/RsyncUI-next/releases).

## Step by step

The pages below follow one session in order: estimating and synchronizing in the new interface, inspecting a task, allowing it in Shortcuts, running it from the Shortcuts app, and checking the result.
