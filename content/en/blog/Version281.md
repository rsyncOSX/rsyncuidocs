+++
author = "Thomas Evensen"
title = "Version 2.8.1"
date = "2025-12-03"
tags = ["changelog","version 2.8.1"]
categories = ["changelog"]
+++

### Version 2.8.1 (build 172) - not yet released

Some info about the *no stats, no log* issue. 

*Updates after some testing this evening, local time*

There are both positive and negative aspects to consider. On the positive side, I have successfully identified the occurrence of the issue and can notify the user accordingly. However, I am **unable** to modify the `try? await Task.sleep(nanoseconds: sleeptime)` code to resolve the problem. To be candid, I am somewhat perplexed as to why this issue arises. Nevertheless, the positive aspect is that RsyncUI is actively notifying the user, and the user has the ability to initiate a synchronization manually when the issue occurs. 

*In the upcoming maintenance release, version 2.8.1, an alert will be introduced to notify users when RsyncUI detects a lack of data to write logdata.*

<div class="alert alert-danger" role="alert">

If you encounter this issue, the data is synchronized, but RsyncUI is reporting a missing loggdata file. For your safety confirm data synchronization, perform another estimate and execute or force an execute without estimation.

</div>

In the upcoming version of RsyncUI, a new error will be introduced. If logging fails due to the aforementioned reason, this error will be generated.

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}

If the issue occurs the log records is set to default values.

{{< figure src="/images/gettingstarted/nostats2.png" alt="" position="center" style="border-radius: 8px;" >}}
