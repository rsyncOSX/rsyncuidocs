+++
author = "Thomas Evensen"
title = "Version 2.7.6"
date = "2025-11-03"
tags = ["changelog","version 2.7.6"]
categories = ["changelog"]
+++

### Version 2.7.6 (build 167) - 3 November, 2025

A few users have experienced a crash when estimating tasks. The release fixes the issue.

{{< alert color="warning" >}}

The update does the following: 

- preventing RsyncUI from crashing when the termination signal is received before all data is read from the datahandle
- the process object also now determines if there is still data to be retrieved after the termination signal is discovered
	- although the reason for this is unknown, it does sometimes happen
- the estimation speed is increased
	- the speed increase is due to more responsive handling of output from rsync and termination signal
    - the actual speed of synchronization of data is **not** changed, that is outside RsyncUI 

{{< /alert >}}

