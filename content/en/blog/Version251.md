+++
author = "Thomas Evensen"
title = "Version 2.5.1"
date = "2025-05-05"
tags = ["changelog","version 2.5.1"]
categories = ["changelog"]
+++

### Version 2.5.1 (build 143) -release candidate

This will stay as a release candidate for some weeks. I need some feedback on the Calendar part before making it a release, most likely in beginning of June 2025.

Major updates in this rc are:

- a new calendar for schedule actions, please read about the scheduler below before commence using it
    - to delete a schedule, just select it and press the back space button
- German and Norwegian localization are deleted
- the Verify a remote function is slightly changed

The scheduler is an easy to use and simple timer based trigger for synchronize data. The synchronize of data is triggered by the same method, URL-action, as for executing a synchronize data either by Widget or by external URL.

{{< alert >}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."*  The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 

Its primary function is to automate selected synchronization of tasks as long as RsyncUI is alive. It *may* prove useful for users who require scheduled  synchronization of data during work. 

RsyncUI may be minimized or not the active window and the timer will still work. But if you leave your Mac and it goes to sleep, the timer will not work.

{{< /alert >}}

The Norwegian and German localization are also been deleted from this version. Regrettably, due to my limited proficiency in German, I am unable to provide a comprehensive translation in German. From this version, RsyncUI speaks English only. 

{{< figure src="/images/251/calendar.png" alt="" position="center" style="border-radius: 8px;" >}}
