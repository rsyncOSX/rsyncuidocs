+++
author = "Thomas Evensen"
title = "Version 2.7.6"
date = "2025-10-31"
tags = ["changelog","version 2.7.6"]
categories = ["changelog"]
+++

### Version 2.7.6 (build 167) - 31 October, 2025 

The rc is removed, still need some more time to fix and update. I anticipate finding a solution to this issue within the beginning of next week. If any users have experienced crashes during the estimation process, please inform me. I will provide a temporary build for you.

{{< alert color="info" >}}

To date, I have not finalized the resolution of the issue reported. However, I have made progress in preventing RsyncUI from crashing when the termination signal is received before all data is read from the datahandle. Additionally, I have implemented a temporary fix that is currently applied to the main and version 2.7.6 repositories.

Currently, the process object determines if there is still data to be retrieved after the progress termination is discovered. Although the reason for this occurrence is unknown, it does happen and necessitates handling.

The above developments are promising to make a final fix for the issue.

{{< /alert >}}

A few users have experienced a crash when estimating tasks. I was unable to determine the cause of the issue until yesterday. Yesterday, I successfully induced RsyncUI to crash with the same crash log as reported, which is a promising step towards resolving the issue.

{{< alert color="warning" >}}

The root cause of the problem has been identified, and a temporary solution has been implemented. However, further code updates and additional testing are necessary. Alternative methods have also been evaluated, but none have yet provided a definitive solution to the issue. Consequently, I continue to work on resolving the problem.

{{< /alert >}}

#### AI

I am actively collaborating with two AI services, Claude Code and GitHub Copilot, to identify potential improvements. Their suggestions are being evaluated, and I am testing their recommendations. While some suggestions prove effective, others require manual code adjustments. Each time a fix is implemented, the code undergoes a slight increase in complexity, which I find undesirable.
