+++
author = "Thomas Evensen"
title = "Version 2.7.6"
date = "2025-10-31"
tags = ["changelog","version 2.7.6"]
categories = ["changelog"]
+++

### Version 2.7.6 (build 167) - 31 October, 2025 

A few users have experienced a crash when estimating tasks. I was unable to determine the cause of the issue until yesterday. Yesterday, I successfully induced RsyncUI to crash with the same crash log as reported, which is a promising step towards resolving the issue.

I anticipate finding a solution to this issue within the beginning of next week.

{{< alert color="warning" >}}

To date, I have not yet finalized the resolution of the issue reported but I am close.

I have made progress in preventing RsyncUI from crashing when the termination signal is received before all data is read from the datahandle. 

The process object also now determines if there is still data to be retrieved after the termination signal is discovered. Although the reason for this is unknown, it does sometimes happen and necessitates handling.

The main and version 2.7.6 repositories is updated.

{{< /alert >}}


#### AI

I am actively collaborating with two AI services, Claude Code and GitHub Copilot, to identify potential improvements. Their suggestions are being evaluated, and I am testing their recommendations. While some suggestions prove effective, others require manual code adjustments. Each time a fix is implemented, the code undergoes a slight increase in complexity, which I find undesirable.
