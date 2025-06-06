+++
author = "Thomas Evensen"
date = "2025-01-30"
title =  "Calendar"
tags = ["calendar","schedule"]
categories = ["synchronize"]
+++
{{% pageinfo color="info" %}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."*  The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 

{{< /pageinfo >}}

#### Limitations

Its primary function is to automate selected synchronization of tasks as long as RsyncUI is alive. It *may* prove useful for users who require scheduled  synchronization of data during work.  RsyncUI may be minimized or not the active window and the timer will still work. 

*But if you leave your Mac and it goes to sleep, the timer will not work.*

#### Add schedule

To add a schedule, click on the date, set time and schedule. That is it. When a schedule is active the user is notified by the sidebar or the toolbar when the sidebar is hidden. By right click on a date will present schedules by date.

{{< figure src="/images/calendar/addcalendar.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/calendar/hidesidebar.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Delete schedule

Select the schedule and press the backspace.

{{< figure src="/images/calendar/deletecalendar.png" alt="" position="center" style="border-radius: 8px;" >}}