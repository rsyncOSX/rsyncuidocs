+++
author = "Thomas Evensen"
title = "Version 2.7.6"
date = "2025-10-30"
tags = ["changelog","version 2.7.6"]
categories = ["changelog"]
+++

### Version 2.7.6 (build 167) - 30 October, 2025 

The rc is removed, still need some more time to fix and update

A few users have experienced a crash when estimating tasks. I was unable to determine the cause of the issue until yesterday. Yesterday, I successfully induced RsyncUI to crash with the same crash log as reported, which is a promising step towards resolving the issue.

{{< alert color="warning" >}}

The root cause of the problem has been identified, and a temporary solution has been implemented. However, further code updates and additional testing are necessary. Alternative methods have also been evaluated, but none have yet provided a definitive solution to the issue. Consequently, I continue to work on resolving the problem.

{{< /alert >}}
