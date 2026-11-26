+++
author = "Thomas Evensen"
title = "Tasks and the task inspector"
linkTitle = "2. Task inspector"
date = "2026-11-26"
weight = 20
description = "The Tasks workspace and the General, Rsync Options and Logs tabs of the inspector."
tags = ["version 4.0.0"]
categories = ["version 4.0.0"]
+++

## General

{{< figure src="/images/version400/nr3.png" alt="Task inspector, General tab" position="center" style="border-radius: 8px;" >}}

In **Tasks**, selecting a task opens the inspector on the right. The **General** tab holds the Synchronize ID, the trailing slash on the source folder, source and destination folders, remote user and server, and the button for the RsyncUI Widget URL. New tasks are created with **Add Task** in the toolbar.

## Rsync Options

{{< figure src="/images/version400/nr4.png" alt="Task inspector, Rsync Options tab" position="center" style="border-radius: 8px;" >}}

The **Rsync Options** tab lists additional rsync arguments (here exclude rules), the SSH connection settings and the *Destination behavior*. When **Delete destination items missing from the source** (`--delete`) is on, a red warning says that synchronization may remove files from the destination.

## Logs

{{< figure src="/images/version400/nr5.png" alt="Task inspector, Logs tab" position="center" style="border-radius: 8px;" >}}

The **Logs** tab shows the run history of the selected task: date, number of files, size and time used. The footer shows the number of log records for the task.
