+++
author = "Thomas Evensen"
title = "Getting started"
date = "2025-02-12"
tags = ["getting started"]
categories = ["general information"]
+++

For new users, kindly refer to the *Important* section. Additionally, please find information about the latest version of rsync to install, refer to the *Latest version of rsync* section .

The primary Sidebar menu is context-sensitive. The rationale behind a context-sensitive Sidebar menu is to conceal menu options that may be distracting to the user.  See last on this page about the sidebar menu options.

#### New Tasks and Verification

RsyncUI supports synchronizing data to:

- local attached disk
- remote servers on the Internet or local LAN
    - requiere *passwordless login*  by ssh-key

##### Local attached disk

RsyncUI can synchronize your data to a local attached disk. If you only want to synchronize data to a local attached disk, connect the disk, add the source and destination, and you are ready for your first task.

##### Remote server and passwordless login

If you want to synchronize data to a server, on the Internet, or your local LAN, there is some more setup to do. If you have enabled *passwordless login* by ssh-key, you only have to add *source*, *destination*, *login id*, and *servername* and you are ready to synchronize data. If you have *not* enabled passwordless login, there are some more actions required before your first task.

##### Verify new tasks

*Always* verify a new task. After adding a task, you can execute a `--dry-run` by double-clicking on the task in the main view. The second subsequent double-click will execute the real task, which is synchronize data from local to remote.

{{< alert color="warning" >}}

A verification of a new task can also be executed by opening the Tasks or Rsync parameters view from the main sidebar, selecting the task, and choosing the "play" icon on the toolbar. This action will execute an estimation run, a \`--dry-run\`, to verify the task.

{{< /alert >}}

**Verify a task in Tasks**

After adding a task, select the task and press the `play`button on the toolbar which are marked in screen dump below. 

{{< figure src="/images/verifyatask/verifytask.png" alt="" position="center" style="border-radius: 8px;" >}}

*Note: The Add and Update button is in next version (not yet released) moved to view from the toolbar.*

**Verify a task in Rsync parameters**

After adding parameters, select the task and press the `play`button on the toolbar which are marked in screen dump below.

{{< figure src="/images/verifyatask/verifyparameter.png" alt="" position="center" style="border-radius: 8px;" >}}

*Note: The Add  button is in next version (not yet released) moved to view from the toolbar.*

##### Aborting tasks

Please note that this is an external task not controlled by RsyncUI, which executes the command-line tool `rsync`. RsyncUI monitors the task for progress and termination.

The user can abort a task at any time. However, it is essential to allow the task to complete and perform any necessary cleanup operations before starting a new task. This process may take a few seconds, and if not, the applications may become unresponsive.

#### The Sidebar Menu options

There are three Sidebar menu options that are contingent upon the properties of a task. It is sufficient as long as one of the tasks satisfies one of the prerequisites.

- *Snapshot*: this option is exclusively available for snapshot tasks
- *Restore*: this option is only available for synchronize- and snapshot tasks where *the destination* is located on a *remote server*
- *Verify remote*: this option is only available for synchronize tasks where *the destination* is located on a *remote server*


