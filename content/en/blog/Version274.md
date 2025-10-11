+++
author = "Thomas Evensen"
title = "Version 2.7.4"
date = "2025-10-11"
tags = ["changelog","version 2.7.4"]
categories = ["changelog"]
+++

### Version 2.7.4 (build 165) - released as rc

Minor updates to RsyncUI have commenced and will be released later in October 2025. Regular updates will be provided as RC releases. The following are the current code changes:

#### October 11, 2025 (in code, not yet released as rc)

The schedule is currently in development and some parts has not yet been released. Dates added to the schedule are validated, and the next schedule added must be *x minutes* ahead of the previous schedule. The Schedule view highlights invalid dates in *red font* and does not display popups if not validated. If a date is not validated, it is not added to the schedule. 	

#### October 11, 2025

- in Settings view, all toggles are changed to `.toggleStyle(.switch)`
- every `.onAppear {...}` is replaced with `.task {...}` if the closure includes asynchronous code
	- the .task modifier handles asynchronous functions directly
- the Schedule function is enhanced to tolerate when the Mac goes to sleep
	- when a scheduled task is not executed when the Mac enters sleep mode, the Schedule function retrieves the unexecuted task and executes it upon the Mac's subsequent wake-up	
