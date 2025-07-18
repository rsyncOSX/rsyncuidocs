+++
author = "Thomas Evensen"
title = "Getting started"
date = "2025-02-12"
tags = ["getting started"]
categories = ["general information"]
+++

For new users, kindly refer to the *Important* section. Additionally, please find information about the latest version of rsync to install, refer to the *Latest version of rsync* section .

The primary Sidebar menu is context-sensitive. The rationale behind a context-sensitive Sidebar menu is to conceal menu options that may be distracting to the user.  See last on this page about the sidebar menu options.

### New Tasks and Verification

RsyncUI supports synchronizing data to:

- local attached disk
- remote servers on the Internet or local LAN
    - requiere *passwordless login*  by ssh-key

#### Local attached disk

RsyncUI can synchronize your data to a local attached disk. If you only want to synchronize data to a local attached disk, connect the disk, add the *source* and *destination*, and you are ready for your first task.

#### Remote server and passwordless login

If you want to synchronize data to a server, on the Internet, or your local LAN, there is some more setup to do. If you have enabled *passwordless login* by ssh-key, you only have to add *source*, *destination*, *login id*, and *server name* and you are ready to synchronize data. If you have *not* enabled passwordless login, there are some more actions required before your first task.

**Verify tasks**

{{< alert color="warning" >}}

*Always* verify a new task. After adding a new task, changed a task, added your own or changed parameters to rsync , select the *"Verify tasks"* from the primary Sidebar menu. 

{{< /alert >}}

 Select the task and press the *play* button on the toolbar. Executing the *play* button includes the --dry-run parameter for rsync, which is an estimation run.

{{< figure src="/images/verifyatask/verifytask.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Aborting tasks

Please note that this is an external task not controlled by RsyncUI, which executes the command-line tool `rsync`. RsyncUI monitors the task for progress and termination.

The user can abort a task at any time. However, it is essential to allow the task to complete and perform any necessary cleanup operations before starting a new task. This process may take a few seconds, and if not, the applications may become unresponsive.

### The Sidebar Menu options

There are three Sidebar menu options that are contingent upon the properties of a task. It is sufficient as long as one of the tasks satisfies one of the prerequisites.

- *Snapshot*: this option is exclusively available for snapshot tasks
- *Restore*: this option is only available for synchronize- and snapshot tasks where *the destination* is located on a *remote server*
- *Verify remote*: this option is only available for synchronize tasks where *the destination* is located on a *remote server*

{{< alert >}}

The Sidebar menu may be hidden, either click on the Hide Sidebar icon top left or toggle ON  *Hide the Sidebar on startup* within the *RsyncUI settings*.

{{< /alert >}}



