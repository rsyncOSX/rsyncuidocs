+++
author = "Thomas Evensen"
title = "Version 2.7.4"
date = "2025-10-21"
tags = ["changelog","version 2.7.4"]
categories = ["changelog"]
+++

### Version 2.7.4 (build 165) - October 21, 2025

The following are updated, including some other cleanups of code (please see [the details about changed files](https://github.com/rsyncOSX/RsyncUI/compare/v2.7.3...v2.7.4)):

In the process of refactoring the Schedule code, I discovered that the model was too fragmented. Consequently, I have refactored most of the model code for Schedule. The UI component remains unchanged. The refactoring process is completed in two stages:

- refactoring the code as it currently functions in the present release, without any improvements for sleep and wakefulness
- refactoring the code to enhance its functionality for sleep and wakefulness

Tasks added to the schedule are validated. The planned next task schedule added must either:

- be *10 minutes ahead* of the first schedule in queue
	- the first schedule in queue is always ahead of now	
- be *10 minutes subtracted* from the first schedule in queue
	- as above, the planned next schedule must also be greater than now
- the Schedule function is enhanced to tolerate when the Mac goes to sleep
	- when a scheduled task is not executed when the Mac enters sleep mode, the Schedule function retrieves unexecuted task and display the tasks in a table
    - the user may move the unexecuted tasks to the schedule table

The Schedule view visually distinguishes invalid times in red font, eliminating the need for additional popups. Only validated task schedules are subsequently incorporated into the schedule.

- in Settings view, all toggles are changed to `.toggleStyle(.switch)`
- every `.onAppear {...}` is replaced with `.task {...}` if the closure includes asynchronous code
	- the .task modifier handles asynchronous functions directly

#### AI and RsyncUI

I have commenced experimenting with artificial intelligence (AI) in coding, specifically utilizing Copilot (GPT-5), a service accessible on GitHub and Claude AI by Anthropic. I am permitted to utilize Copilot for free due to the open-source nature of RsyncUI. Claude AI offers a free version with limitations on the number of questions asked within a specified time frame. I inquired with Copilot and Claude AI about optimizing the Schedule code to enhance its reliability during sleep mode on macOS. I am genuinely impressed by the capabilities of AI in assisting with coding tasks.

Additionally, I am employing artificial intelligence to review my code and make necessary enhancements.

#### Issues when testing awake on Mac

During the testing of the revised code, I encountered an issue with the Mac's behavior when it returns from being asleep and an external attached disc is present. Upon waking, the Mac ejects the attached volume, which subsequently disrupts the synchronization process of RsyncUI. You may test this yourself to verify if there is an issue regarding this.

I asked ChatGPT about this and the answer was: *"Your Mac ejects external disks when waking from sleep due to a common bug or power management issue, where the system incorrectly unmounts the drive during the sleep-wake cycle. To fix this, you can update your macOS, adjust energy saver settings, check for issues with hubs or docks, or use a third-party app like Jettison to automatically unmount the drive before sleep and remount it upon waking."*
