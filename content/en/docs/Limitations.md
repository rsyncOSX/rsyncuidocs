+++
author = "Thomas Evensen"
title = "Limitations"
date = "2025-03-22"
tags = ["limitations"]
categories = ["general information"]
+++

There are a few limitations or constraints to be aware of when using RsyncUI. None of these limitations can result in data corruption or trouble. However, they may inadvertently halt an ongoing synchronization process.

### Long running tasks and sleep

Upon each Mac sleep, RsyncUI synchronization tasks cease. An active rsync process does not prevent the Mac from sleeping. If the Mac sleeps during a synchronization task, rsync likely generates an error, halting the task. The only method to resume synchronization is to restart it via RsyncUI. RsyncUI will resume and synchronize data not yet transferred. Rsync is adept and resumes from its previous state.

If the above occurs, RsyncUI will not generate any logs. RsyncUI logs only upon detecting a termination signal from rsync. If the Mac enters sleep during data synchronization, there will be no termination signal and no logging by RsyncUI.

{{< alert >}}

You may modify your Mac's sleep settings to control when it sleeps.

{{< /alert >}}

The above will also be true if you are using the Calendar function.

### The Schedule

A note about the Schedule and scheduling of actions. There are some limitations on how the scheduler works due to how the Timer library is developed. Refer to the *Schedule* section for more information about this function.

Its primary function is to automate synchronization of selected tasks as long as RsyncUI is running and you are logged in. It *may* prove useful for users who require scheduled synchronization of data during work. If there are scheduled tasks not executed when the Mac enters sleep mode, they will be explicitly displayed in the Schedule view when the Mac wakes up. 

### Aborting Tasks

Please be cognizant that this is an external task not under the control of RsyncUI. It executes the command-line tool `rsync`. RsyncUI monitors the task for progress and termination.

The user has the authority to abort a task at any time. Please allow the abort process to complete and execute any necessary cleanup operations before initiating a new task. This process may take a few seconds. If you don't wait, RsyncUI may become unresponsive.