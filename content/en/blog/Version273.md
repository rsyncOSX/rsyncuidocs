+++
author = "Thomas Evensen"
title = "Version 2.7.3"
date = "2025-09-25"
tags = ["changelog","version 2.7.3"]
categories = ["changelog"]
+++

### Version 2.7.3 (build 164) - September 26, 2025

There are no model or process updates within this build, only minor GUI updates and fix for the inflect keyword. For comprehensive details regarding the modifications, kindly consult the files that underwent changes within the [release page](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.7.3).

New updates in code are:

- version Xcode 26.01 is released, new build will be with updated Xcode
- there logical error in the min/hour/day variable in dev builds are fixed, the plurals are now accurate
- cleaning up and hiding details in *Tasks* and *Rsync parameters* view, hide distracting details
	- details may be enabled by a toggle
    - objective is to keep views as clean and simple as possible
- the issue with plurals and the `inflect` keyword has been resolved, plurals are now managed manually
