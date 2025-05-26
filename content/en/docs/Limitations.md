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

#### The Calendar

A note about the Calendar and schedule of actions. There are limitations of how the scheduler works due to how the Timer library is developed. Refer to the blog *Timer and Calendar* for more detailed info about the Timer.

Its primary function is to automate selected synchronization of tasks as long as RsyncUI is alive and you are logged in. It *may* prove useful for users who require scheduled  synchronization of data during work.  RsyncUI may be minimized or not the active window and the timer will still work. 

{{< alert >}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."* 

If you leave your Mac and it goes to sleep, the timer will *not work*.

{{< /alert >}}

The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 



### Aborting Tasks

Please be cognizant that this is an external task not under the control of RsyncUI. It executes the command-line tool `rsync`.
RsyncUI monitors the task for progress and termination.

The user has the authority to abort a task at any juncture. Please permit the abort to complete and execute any necessary cleanup operations before initiating a new task. This process may take a few seconds. If not, RsyncUI may become unresponsive.
