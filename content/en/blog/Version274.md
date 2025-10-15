+++
author = "Thomas Evensen"
title = "Version 2.7.4"
date = "2025-10-15"
tags = ["changelog","version 2.7.4"]
categories = ["changelog"]
+++

### Version 2.7.4 (build 165) - not yet released as rc

Minor updates to RsyncUI have commenced and will be released later in October 2025. The following are the current updates:

#### October 15, 2025

{{< alert color="warning" >}}

Despite ongoing discussions with AI, when I request code simplification for GlobalTimer.swift, I still encounter code modifications. I intend to apply these changes to the version 2.7.4 branch and conduct further testing before preparing a new release candidate. The previous release candidate has been removed, as it appears to function correctly, but the code in GlobalTimer.swift remains overly complex. 

{{< /alert >}}

I have commenced experimenting with AI in coding, specifically using Copilot (GPT-5), a service available on GitHub. I am permitted to utilize Copilot for free due to the open-source nature of RsyncUI. I inquired with Copilot about optimizing the [GlobalTimer.swift](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Global/GlobalTimer.swift) to enhance its reliability during sleep mode on macOS. I was genuinely impressed by the capabilities of AI in assisting with coding tasks. After engaging in a series of discussions with Copilot, I have come to the conclusion that the Schedule function has been improved in terms of reliability.

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
