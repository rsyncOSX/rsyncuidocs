+++
author = "Thomas Evensen"
title = "Version 2.5.0"
date = "2025-04-24"
tags = ["changelog","version 2.5.0"]
categories = ["changelog"]
+++

### Version 2.5.0 (build 142) - work in progress

The development of a scheduler is progressing slowly, but steadily. The plan includes a scheduled backup function to RsyncUI. Recent development has been limited. During the spring and summer months, I prioritize capturing bird photographs. There may be some development during these periods, but the plan remains to release a new version after summer. It is also beneficial to periodically cease development and allow for catch-up. 

The scheduler will maintain a single schedule at a time. Upon completion of the scheduled action, the scheduler will transition to the next scheduled action and continue tracking it. The calendar view itself does not store any schedules. Instead, it calculates scheduled dates based on the schedule table and marks them yellow. This approach aims to minimize memory usage and resources while keeping track of schedules.

The scheduler is not an advanced scheduling tool. Its primary function is to automate selected synchronization tasks as long as RsyncUI is in operation. It *may* prove useful for users who require regular data synchronization during their work.

The Norwegian and German localization has been removed from this version. Regrettably, due to my limited proficiency in German, I am unable to provide a comprehensive translation in German. From this version, RsyncUI speaks English only. 

{{< figure src="/images/250/calendar.png" alt="" position="center" style="border-radius: 8px;" >}}

##### Calendar app

In the process of developing the calendar and schedule functionalities for RsyncUI, I have been primarily working on a separate Calendar application. RsyncUI does support incoming URL commands. When the calendar function triggers an action, it generates an URL command for estimating and executing the actual profile. 

-  the URL for the default profile is as follows: `rsyncuiapp://loadprofileandestimate?profile=default`
-  the Calendar application will actually open RsyncUI by executing the command `NSWorkspace.shared.open(URL(string: url.absoluteString)!)`
 
Consequently, the Calendar application *may* also serve as *a standalone* schedule application for RsyncUI. 

{{< figure src="/images/250/calendarapp.png" alt="" position="center" style="border-radius: 8px;" >}}

