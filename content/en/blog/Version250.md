+++
author = "Thomas Evensen"
title = "Version 2.5.0"
date = "2025-05-02"
tags = ["changelog","version 2.5.0"]
categories = ["changelog"]
+++

### Version 2.5.0 (build 142) - work in progress

The development of a scheduler is working as a beta version. The scheduler is an easy to use and simple timer based trigger for synchronize data. The synchronize of data is triggered by the same method, URL-action, as for executing a synchronize data either by Widget or by external URL.

If you want to try out the scheduler, please drop me an e-mail. You may find my e-mail in the About section.

{{< alert >}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."*  The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 

Its primary function is to automate selected synchronization tasks as long as RsyncUI is alive. It *may* prove useful for users who require scheduled  synchronization of data during work. 

RsyncUI may be minimized or not the active window and the timer will work. But if you leave your Mac and it goes to sleep, the timer will not work.

{{< /alert >}}


During the spring and summer months, I prioritize capturing bird photographs. There is some development during these periods, but the plan remains to release a new version later in summer. It is also beneficial to periodically cease development and allow for catch-up. 

The Norwegian and German localization are also been removed from this version. Regrettably, due to my limited proficiency in German, I am unable to provide a comprehensive translation in German. From this version, RsyncUI speaks English only. 

{{< figure src="/images/250/calendar.png" alt="" position="center" style="border-radius: 8px;" >}}
