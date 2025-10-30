+++
author = "Thomas Evensen"
title = "Version 2.7.6"
date = "2025-10-30"
tags = ["changelog","version 2.7.6"]
categories = ["changelog"]
+++

### Version 2.7.6 (build 167) - 30 October, 2025 release candidate

Please download and test the rc.

A few users have experienced a crash when estimating tasks. I was unable to determine the cause of the issue until yesterday. Yesterday, I successfully induced RsyncUI to crash with the same crash log as reported, which is a promising step towards resolving the issue.

{{< alert color="warning" >}}

It is of utmost importance that the updated code functions as intended. A release candidate for testing purposes has been released. In addition to resolving the identified issue, the updated code introduces an enhancement in both data estimation and synchronization. 

The increased speed observed in RsyncUI’s data reading from the rsync process is not directly related to the actual synchronization of data, which is managed independently of RsyncUI.

{{< /alert >}}
