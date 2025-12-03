+++
author = "Thomas Evensen"
title = "Version 2.8.1"
date = "2025-12-03"
tags = ["changelog","version 2.8.1"]
categories = ["changelog"]
+++

### Version 2.8.1 (build 172) - not yet released

Some info about the *no stats, no log* issue.

*In the upcoming maintenance release, version 2.8.1, an alert will be introduced to notify users when RsyncUI detects a lack of data to write logdata. While still in development, RsyncUI in version 2.8.1 will now throw an error when this condition is met. Notably, the loop for executing and estimating will continue to run even after the error is encountered.*

It appears that the issue is only on my Mac Mini M4 and does not manifest on my MacBook Pro M3. Furthermore, the issue only occurs when synchronizing a small amount of data to a fast local attached SSD. And it is only when running RsyncUI as an application compiled for release that this error is encountered.

I am unable to produce this error when executing RsyncUI within Xcode. Executing RsyncUI within Xcode results in increased code execution time, and the summarized output from rsync is captured when the termination signal is detected.

The SPM RsyncProcess, in development, has been enhanced to apply a new value to the `try? await Task.sleep(nanoseconds: sleeptime)` function. This modification increasing sleeptime for the termination signal, by default set to 50,000,000 nanoseconds (50 milliseconds).

During development, I will intentionally recreate the issue. Furthermore, by increasing the Task.sleep value, I will attempt to resolve the issue. If this resolves the issue, I will make an input in the settings during the upcoming maintenance release to update the default sleeptime. The updated sleeptime will be stored as part of RsyncUI settings.

<div class="alert alert-danger" role="alert">

If you encounter this issue, the data is synchronized, but RsyncUI is reporting a missing loggdata file. For your safety confirm data synchronization, perform another estimate and execute or force an execute without estimation.

</div>

In the upcoming version of RsyncUI, a new error will be introduced. If logging fails due to the aforementioned reason, this error will be generated.

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}
