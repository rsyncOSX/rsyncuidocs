+++
author = "Thomas Evensen"
title = "Getting started"
date = "2025-02-12"
tags = ["getting started"]
categories = ["general information"]
+++

For new users, kindly refer to the *Important* section. Additionally, please refer to the *Latest version of rsync* section for information about installing the latest version.

### Concealing Actions

The rationale behind concealing actions is to minimize clutter in menus and enhance user focus.

By utilizing the shortcut `⌘S` (for displaying or hiding) or accessing the Task main menu, the Charts, Quick task, view logfile, and several other options will be revealed. These options are concealed by default. To reveal them, simply toggle the show or hide option using the shortcut.

The primary Sidebar menu is also context-sensitive. Refer to the concealing options mentioned at the end of this page for further details.

### New Tasks and Verification

RsyncUI supports synchronizing data to:

- local attached disk
- remote servers on the Internet or local LAN
    - require *passwordless login* by ssh-key

#### Local attached disk

RsyncUI can synchronize your data to a local attached disk. If you only want to synchronize data to a local attached disk, connect the disk, add the *source* and *destination*, and you are ready for your first task.

#### Remote server and passwordless login

If you want to synchronize data to a server, on the Internet, or your local LAN, there is some more setup to do. If you have enabled *passwordless login* by ssh-key, you only have to add *source*, *destination*, *login id*, and *server name* and you are ready to synchronize data. If you have *not* enabled passwordless login, there are some more actions required before your first task.

**Verify tasks**

<div class="alert alert-danger" role="alert">

*Always* verify a new task. After adding a new task, changing a task, or adding your own or changed parameters to rsync, select *"Verify tasks"* from the primary Sidebar menu. 

</div>

Select the task and press the *play* button on the toolbar. Executing the *play* button includes the --dry-run parameter for rsync, which is an estimation run.

{{< figure src="/images/verifyatask/verifytask.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Aborting tasks

Please note that this is an external task not controlled by RsyncUI, which executes the command-line tool `rsync`. RsyncUI monitors the task for progress and termination.

The user can abort a task at any time. However, it is essential to allow the task to complete and perform any necessary cleanup operations before starting a new task. This process may take a few seconds, and if you don't wait, the application may become unresponsive.

### There are errors in tagging data

Sometimes you may get the error:
```
There are errors in tagging data
for synchronize ID XXXX
Most likely number of rows
> 20 lines and no data to synchronize
```

The preceding message serves as a cautionary note and a confirmation that all data has been synchronized. RsyncUI provides an indication of whether there is data to be transferred. Typically, the output from rsync is less than 20 rows if no data synchronization is required. 

Please refer to the following for further clarification: RsyncUI analyzes the summary output from rsync to identify data that needs to be synchronized or not. Occasionally, RsyncUI may detect that the number of lines from rsync exceeds 20, yet it still tags the data as not needing synchronization. This message serves as a reminder to verify that all data has been successfully synchronized. 

To clarify this message, select the task and execute it, or synchronize it, without providing an estimate. 

Version 3.x of rsync:

{{< figure src="/images/gettingstarted/linesver3x.png" alt="" position="center" style="border-radius: 8px;" >}}

Version openrsync:

{{< figure src="/images/gettingstarted/linesopenrsync.png" alt="" position="center" style="border-radius: 8px;" >}}

### Concealing Options

#### The Sidebar Menu options

There are three Sidebar menu options that are contingent upon the properties of a task. It is sufficient as long as one of the tasks satisfies one of the prerequisites.

- *Snapshot*: this option is exclusively available for *snapshot* tasks
	- requires version 3.x of rsync
- *Restore*: this option is only available for *synchronize* and *snapshot* tasks where *the destination* is located on a *remote server*	
	- available for openrsync as well, but only for synchronize tasks
- *Verify remote*: this option is only available for *synchronize* tasks where *the destination* is located on a *remote server*
	- requires version 3.x of rsync

<div class="alert alert-secondary" role="alert">

The Sidebar menu may be hidden, either click on the Hide Sidebar icon top left or enable *Hide the Sidebar on startup* within the *RsyncUI settings*.

</div>

#### The menu bar

Toggle the shortcut `⌘S`:

{{< figure src="/images/gettingstarted/hidden.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/gettingstarted/presented.png" alt="" position="center" style="border-radius: 8px;" >}}

