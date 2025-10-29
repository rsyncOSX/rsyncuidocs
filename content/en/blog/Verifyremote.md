+++
author = "Thomas Evensen"
title = "Verify remote"
date = "2025-10-27"
tags = ["verify remote"]
categories = ["technical details"]
+++

### Verify remote

This blog is how I am using the *Verify remote* function. 

#### The remote 

I am backing up my bird photography on multiple devices:

- A Raspberry Pi5 server located at a remote server, configured with two WD Red SA500 2.5" SSD 1TB drives set up as a mirrored ZFS pool.
- To a remote cloud service (JottaCloud).
- Lastly, two 1TB NVMe external SSD drives attached to my computer.

The first two devices are updated whenever data is updated. Updating JottaCloud is managed by a service on my MacBooks. Updates to the Raspberry Pi5 server are performed using RsyncUI.

Currently, my bird photography data consists of 140GB of data and 8000 files, including RAW and sidecar files. During travel, I utilize my MacBook Pro for photo editing, while at home, I use my Mac Mini M4. I always keep track of which Mac is updated and stores the most recent files and updates.

For this blog post, I am using my MacBook Pro as the local device, while the remote server contains more updated data.

#### The requirements for using Verify remote

{{< alert color="warning" >}}

The user is solely responsible for determining the appropriate action. RsyncUI provides only advisory guidance, based on a rudimentary evaluation of a push and pull data comparison. Additionally, the function requires version 3.x of rsync to be installed and enabled.

The Verify process necessitates that one of the Macs be synchronized with the remote. If both Macs have local unique updates, the outcome of the Verify is most likely inaccurate, potentially resulting in data loss.

The function is not intended to be automated. Users must verify their subsequent actions. 

{{< /alert >}}

#### The procedure

Select the picture profile that stores my task to synchronize my local picture raw catalog with my remote server. After selecting the task, open the Verify remote function.

{{< figure src="/images/verifyremote/main.png" alt="" position="center" style="border-radius: 8px;" >}}

During the initial run, the *Adjust output* toggle is disabled. When enabled, the function eliminates the last 16 lines of output from both pull and push operations, as well as all other lines that are identical in both operations. To initiate the evaluation, select the upward arrow.

{{< figure src="/images/verifyremote/start.png" alt="" position="center" style="border-radius: 8px;" >}}

The remote server has less data than my local Mac because I deleted some photos that are synced to the remote. The output from rsync is tagged with some information, which is evaluated by looking at the first characters of the output. The push data on the left table indicates that my local Mac contains more data, which I know because the remote is updated with deleted photos.

{{< figure src="/images/verifyremote/result1.png" alt="" position="center" style="border-radius: 8px;" >}}

The *Adjust output* toggle is enabled, a new evaluation is commenced.

{{< figure src="/images/verifyremote/start2.png" alt="" position="center" style="border-radius: 8px;" >}}

The remote table on the right indicates that there are updates to sidecars and local data that need to be deleted. 

{{< figure src="/images/verifyremote/result2.png" alt="" position="center" style="border-radius: 8px;" >}}

I make a pull data from remote to update my local Mac. 

{{< figure src="/images/verifyremote/pull.png" alt="" position="center" style="border-radius: 8px;" >}}

Following the pull, the Verify remote displays my local Mac and remote device in sync.

{{< figure src="/images/verifyremote/afterpull.png" alt="" position="center" style="border-radius: 8px;" >}}
