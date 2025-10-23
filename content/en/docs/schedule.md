+++
author = "Thomas Evensen"
date = "2025-01-30"
title =  "Schedule"
tags = ["schedule"]
categories = ["synchronize"]
+++

{{< alert >}}

 The schedule function is by default disabled. Please refer to section *RsyncUI settings, Monitor and log* to enable.

{{< /alert >}}

Schedules are automatically saved to disk. RsyncUI loads the schedule file and reloads tasks that are due. Tasks scheduled to execute when the Mac is shut down are not loaded. If the Mac is put into sleep mode, RsyncUI will display unexecuted tasks in the Schedule view. There is *no automatic execution* of scheduled tasks that have not been executed. 

{{< alert >}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."*  The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 

If scheduled tasks are not executed when the Mac enters sleep mode, they will be displayed within the Schedule view. 

{{< /alert >}}

#### Add schedule

To add a schedule, click on the date, set time and schedule. That is it. When a schedule is active the user is notified by the sidebar or the toolbar when the sidebar is hidden. By right click on a date will present schedules by date.

Tasks added to the schedule are validated. The planned next task schedule added must either:

- be *10 minutes ahead* of the first schedule in queue
	- the first schedule in queue is always ahead of now	
- be *10 minutes subtracted* from the first schedule in queue
	- as above, the planned next schedule must also be greater than now
- the Schedule function is enhanced to tolerate when the Mac goes to sleep
	- when a scheduled task is not executed when the Mac enters sleep mode, the Schedule function retrieves unexecuted task and display the tasks in a table
    - the user may move the unexecuted tasks to the schedule table

The Schedule view visually distinguishes invalid times in red font. Only validated task schedules are subsequently incorporated into the schedule.

{{< figure src="/images/calendar/addcalendar.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/calendar/hidesidebar.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Delete schedules

Select the schedules, one or more, and press the backspace.

{{< figure src="/images/calendar/deletecalendar.png" alt="" position="center" style="border-radius: 8px;" >}}