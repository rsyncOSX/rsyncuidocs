+++
author = "Thomas Evensen"
title = "Version 2.7.2"
date = "2025-09-25"
tags = ["changelog","version 2.7.2"]
categories = ["changelog"]
+++

### Version 2.7.2 (build 163), dev build 3 - September 25, 2025

Update: There is one logical error in the min/hour/day variable, which has been corrected in *the code*. The plurals are now accurate. 

There are no model or process updates within this build, only minor GUI updates and fix for the inflect keyword. For comprehensive details regarding the modifications, kindly consult the files that underwent changes within the [release page](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.7.2b3).


#### September 25

Most likely the last dev build before a new release. 

New updates in code are:

- version Xcode 26.01 is released, new build will be with updated Xcode
- cleaning up and hiding details in *Tasks* and *Rsync parameters* view, hide distracting details
	- details may be enabled by a toggle
    - objective is to keep views as clean and simple as possible

#### September 23

In Swift 6.2 on macOS Tahoe 26, the issue with plurals and the `inflect` keyword has been resolved. Plurals are now managed manually. Additionally, there are some other GUI updates, including the display of minutes, hours, or days with correct plurals.
