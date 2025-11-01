+++
author = "Thomas Evensen"
title = "Version 2.7.6"
date = "2025-11-01"
tags = ["changelog","version 2.7.6"]
categories = ["changelog"]
+++

### Version 2.7.6 (build 167) - 1 November, 2025 release candidate

A few users have experienced a crash when estimating tasks. I was unable to determine the cause of the issue until a couple of days ago. The rc fixes the issue, please test.

{{< alert color="warning" >}}

The update now does the following: 

- preventing RsyncUI from crashing when the termination signal is received before all data is read from the datahandle
- the process object also now determines if there is still data to be retrieved after the termination signal is discovered
	- although the reason for this is unknown, it does sometimes happen

The main and version 2.7.6 repositories is updated.

{{< /alert >}}

#### AI

I am actively collaborating with two AI services, Claude Code and GitHub Copilot, to identify potential improvements. Their suggestions are being evaluated, and I am testing their recommendations. While some suggestions prove effective, others require manual code adjustments. Each time a fix is implemented, the code undergoes a slight increase in complexity, which I find undesirable.
