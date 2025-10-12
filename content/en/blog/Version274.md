+++
author = "Thomas Evensen"
title = "Version 2.7.4"
date = "2025-10-12"
tags = ["changelog","version 2.7.4"]
categories = ["changelog"]
+++

### Version 2.7.4 (build 165)

Minor updates to RsyncUI have commenced and will be released later in October 2025. The following are the current updates:

#### October 12, 2025

Tasks added to the schedule are validated. The planned next task schedule added must either:

- be *x minutes ahead* of the first schedule in queue
	- the first schedule in queue is always ahead of now	
- be *x minutes subtracted* from the first schedule in queue
	- as above, the planned next schedule must also be greater than now

The Schedule view visually distinguishes invalid times in red font, eliminating the need for additional popups. Only validated task schedules are subsequently incorporated into the schedule.

For the moment x is ten minutes.

##### Sleep mode and queued tasks

When the Mac enters sleep mode with scheduled tasks in queue, the last unexecuted task for the specified profile is executed upon the Mac’s subsequent wake-up. If there are multiple unexecuted tasks for a named profile, only the most recent task in the queue is executed. 

#### October 11, 2025

- in Settings view, all toggles are changed to `.toggleStyle(.switch)`
- every `.onAppear {...}` is replaced with `.task {...}` if the closure includes asynchronous code
	- the .task modifier handles asynchronous functions directly
- the Schedule function is enhanced to tolerate when the Mac goes to sleep
	- when a scheduled task is not executed when the Mac enters sleep mode, the Schedule function retrieves the unexecuted task and executes it upon the Mac's subsequent wake-up	
