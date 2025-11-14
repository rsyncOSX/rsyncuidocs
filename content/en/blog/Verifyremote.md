+++
author = "Thomas Evensen"
title = "Verify remote"
date = "2025-10-27"
tags = ["verify remote"]
categories = ["technical details"]
+++

### Overview

This post describes how I use the *Verify remote* function.

### The Remote Setup

I back up my bird photography to multiple locations:

- a Raspberry Pi 5 server configured with two WD Red SA500 2.5" SSD 1TB drives set up as a mirrored ZFS pool
- a remote cloud service (JottaCloud)
- two 1TB NVMe external SSD drives attached to my computers

The first two locations are updated whenever data changes. JottaCloud updates are managed by a service running on my Macs. Updates to the Raspberry Pi 5 server are performed using RsyncUI.

Currently, my bird photography consists of 140GB and 8,000 files, including RAW and sidecar files. During travel, I use my MacBook Pro for photo editing, while at home, I use my Mac Mini M4. I always keep track of which Mac has been updated and stores the most recent files.

For this post, I am using my MacBook Pro as the local device, while the remote server contains more recently updated data.

### Requirements for Using Verify Remote

{{< alert color="warning" >}}

The user is solely responsible for determining the appropriate action. RsyncUI provides only advisory guidance based on a basic evaluation of push and pull data comparison. Additionally, this function requires rsync version 3.x to be installed and enabled.

The Verify process requires that one of the Macs be synchronized with the remote. If both Macs have local unique updates, the Verify outcome is likely inaccurate, potentially resulting in data loss.

This function is not intended to be automated. Users must verify their subsequent actions.

{{< /alert >}}

### The Procedure

Select the Pictures profile that stores my task to synchronize my local picture raw catalog with my remote server. After selecting the task, open the *Verify remote* function.

{{< figure src="/images/verifyremote/main.png" alt="" position="center" style="border-radius: 8px;" >}}

During the initial run, the *Adjust output* toggle is disabled. When enabled, the function eliminates the last 16 lines of output from both pull and push operations, as well as all other lines that are identical in both. To initiate the evaluation, select the upward arrow.

{{< figure src="/images/verifyremote/start.png" alt="" position="center" style="border-radius: 8px;" >}}

The remote server has less data than my local Mac because I deleted some photos locally that were previously synced to the remote. The output from rsync is tagged with information that is evaluated by looking at the first characters of each line. The push data in the left table indicates that my local Mac contains more data, which makes sense because the remote needs to be updated to reflect the deleted photos.

{{< figure src="/images/verifyremote/result1.png" alt="" position="center" style="border-radius: 8px;" >}}

The *Adjust output* toggle is enabled, and a new evaluation begins.

{{< figure src="/images/verifyremote/start2.png" alt="" position="center" style="border-radius: 8px;" >}}

The remote table on the right indicates that there are updates to sidecars and local data that need to be deleted.

{{< figure src="/images/verifyremote/result2.png" alt="" position="center" style="border-radius: 8px;" >}}

I perform a pull of data from the remote to update my local Mac.

{{< figure src="/images/verifyremote/pull.png" alt="" position="center" style="border-radius: 8px;" >}}

Following the pull, *Verify remote* displays that my local Mac and remote device are in sync.

{{< figure src="/images/verifyremote/afterpull.png" alt="" position="center" style="border-radius: 8px;" >}}