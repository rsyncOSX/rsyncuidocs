+++
author = "Thomas Evensen"
title = "Important"
date = "2025-03-22"
tags = ["important"]
categories = ["general information"]
+++

The User Interface of RsyncUI may pose challenges for users unfamiliar with the `rsync` command. The primary objective is to simplify the usage of `rsync`, rather than providing a comprehensive introduction to `rsync` for macOS users. This scope is beyond the intended purpose of the interface. RsyncUI is a graphical layer atop the command-line tool `rsync`. It does not directly perform the underlying operations; `rsync` is responsible for the actual synchronization of data.

<div class="alert alert-danger" role="alert">

Setting incorrect parameters for rsync can result in the deletion of data. Furthermore, RsyncUI does not prevent you from performing such actions. RsyncUI is a complimentary and open-source application. *Kindly review the MIT license* before commencing to use RsyncUI.

</div>

Before executing a new task in RsyncUI, please perform an estimation run, a --dry-run, and inspect the result. If you inadvertently set an empty directory as the source and the *delete parameter* is *enabled*, rsync will delete all files in the destination.

<div class="alert alert-danger" role="alert">

For instructions on how to *verify a task*, new or changed tasks, refer to the *Getting started* or *New tasks* section. 

</div>

### The delete parameter

The --delete parameter, herein referred to as the *delete parameter*, enables rsync to maintain absolute synchronization between the source and destination directories. When a file is deleted from the source, the *delete parameter* instructs rsync to delete the corresponding file from the destination. Conversely, if the *delete parameter* is disabled, the destination directory will contain additional data after deleting files from the source.

Therefore, it is crucial to ascertain whether the *delete parameter* is enabled or disabled. Enabling the *delete parameter* ensures complete synchronization between the source and destination directories.

#### How to remove and add the delete parameter

Select *Rsync parameters* from the primary Sidebar menu. Select the task for which you want to add or remove the `--delete` parameter. Then toggle *Add --delete parameter* (**ON** means added). After toggling, *remember to update the task*.

- if ON, the --delete parameter is included
- if OFF, the --delete parameter is removed

{{< figure src="/images/rsyncparameters/parameters.png" alt="" position="center" style="border-radius: 8px;" >}}

### Temporary halt tasks

A task can be temporarily halted. Within the primary Synchronize view, select the task and right-click. Halting a task will retain the type of task that was halted when the task is resumed. A halted task displays a red stop sign in the action column.

{{< figure src="/images/important/halttask.png" alt="" position="center" style="border-radius: 8px;" >}}

### Two options to save updates to data

This option applies to the data synchronized by RsyncUI. By enabling either of these options, you can save changes to data, such as deletions or updates, prior to a synchronization task.

{{< alert >}}

There are two options to automatically save changes to data when it is changed or deleted. 

**Option 1:** `rsync` supports a *backup* flag. Switching this *on* in the *Rsync parameters* view adds the required parameters. You may change the backup directory to any location you want.  

**Option 2:** Using *snapshots* requires that the latest version 3.x of `rsync` is installed. Please refer to the *Snapshots* section for information on how to enable and use snapshots.

{{< /alert >}}

### Remote servers

RsyncUI compels data transfer via SSH if the destination is a remote server. The parameter `-e ssh` to rsync enables data transfer to be tunneled via SSH. It appears that recent versions of rsync or SSH do not require this parameter, but for safety, RsyncUI appends it if the destination is a remote server.

Through the SSH tunnel, the transfer is encrypted when transmitted over a network connection. Refer to the *Passwordless login* section for further information on SSH and SSH-keys. This feature cannot be disabled.