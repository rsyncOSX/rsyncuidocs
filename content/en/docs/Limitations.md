+++
author = "Thomas Evensen"
title = "Limitations"
date = "2025-03-22"
tags = ["limitations"]
categories = ["general information"]
+++

There are a few limitations or constraints to be aware of when using RsyncUI. NONE of these limitations can result in data corruption or trouble. However, they may inadvertently halt an ongoing synchronization process.

### Long running tasks and sleep

Upon each Mac sleep, RsyncUI synchronization tasks cease. An active rsync process does not prevent Mac sleep. If Mac sleeps during a synchronization task, rsync likely generates an error, halting the task. The sole method to resume synchronization is to restart it via RsyncUI. RsyncUI will resume and synchronize data not yet transferred. Rsync is adept and resumes from its previous state.

If the above occurs, RsyncUI will not generate any logs. RsyncUI logs only upon detecting a termination signal from rsync. If Mac enters sleep during data synchronization, there will be no termination signal and no logging by RsyncUI.

{{< alert >}}

You may modify your Mac's sleep settings to control when it sleeps.

{{< /alert >}}

The above will also be true of you are using the Calendar function.

### The Schedule

A note about the Schedule and scheduling of actions. There are limitations of how the scheduler works due to how the Timer library is developed. Refer to the section *Schedule* for more info about the function.

Its primary function is to automate selected synchronization of tasks as long as RsyncUI is alive and you are logged in. It *may* prove useful for users who require scheduled  synchronization of data during work.  RsyncUI may be minimized or not the active window and the timer will still work. 

{{< alert >}}

In the upcoming release of RsyncUI version 2.7.4, modifications have been made to the Schedule code. As previously mentioned, the Timer library operates only when the Mac is in an awake state. To address this issue, RsyncUI by the Schedule monitors when the Mac enters sleep mode. When the Mac is awake, RsyncUI checks if there are scheduled tasks that have not been executed. If so, RsyncUI executes this task. If there are multiple tasks that have not been executed for a specific profile, RsyncUI executes only one task for that profile. If there are multiple tasks that have not been executed for various profiles, RsyncUI adds a 5-minute delay to the next task to prevent executing more than one task at a time.

This update needs some more testing before new release.

Refer to the section *Schedule* for more info about the function.

{{< /alert >}}

### Aborting Tasks

Please be cognizant that this is an external task not under the control of RsyncUI. It executes the command-line tool `rsync`.
RsyncUI monitors the task for progress and termination.

The user has the authority to abort a task at any juncture. Please permit the abort to complete and execute any necessary cleanup operations before initiating a new task. This process may take a few seconds. If not, RsyncUI may become unresponsive.
