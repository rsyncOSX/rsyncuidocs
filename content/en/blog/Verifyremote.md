+++
author = "Thomas Evensen"
title = "Verify remote"
date = "2025-10-27"
tags = ["verify remote"]
categories = ["technical details"]
+++

### Overview

<div class="alert alert-danger" role="alert">

This function has been removed from RsyncUI version 2.8.6  (January 8, 2026). It will be developed as a standalone application and may delete data if used improperly.

This document to be refactored. 

</div>

This post describes how I use the *Verify remote* function.

### The Remote Setup

I back up my bird photography to multiple locations:

- a Raspberry Pi 5 server configured with two WD Red SA500 2.5" SSD 1TB drives set up as a mirrored ZFS pool
- a remote cloud service (JottaCloud)
- two 1TB NVMe external SSD drives attached to my computers

The first two locations are updated whenever data changes. JottaCloud updates run via a service on my Macs, while RsyncUI updates the Raspberry Pi 5 server.

Currently, my bird photos total 140 GB across 8,000 RAW and sidecar files. I edit on a MacBook Pro while traveling and on a Mac Mini M4 at home. I keep track of which Mac holds the latest edits.

For this walkthrough, the MacBook Pro is local and the remote server has the newer data.

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

<div class="alert alert-danger" role="alert">

Prior to utilizing this function, kindly consult its documentation to ensure you make the appropriate decision.

The Verify remote function helps synchronize multiple Macs to a single remote repository (excluding Git repositories) and update local data from the same remote.

This was built for a personal need. I use two Macs for photo development and synchronize data to a remote folder. The remote is not a Git repository, so a tool was needed to decide whether to push or pull data.

Important: This method requires you to remember which Mac last synced. If not, you risk data loss. Establish a procedure. For example, at home I always use my Mac Mini M4 to edit photos. When traveling, I always use my MacBook Pro, fully synced with my Mac Mini before I leave.

</div>

### From the doc part

Typically, a synchronize action operates in a *one-way* direction of data. Local data is synchronized to a backup media, such as an attached disc or a remote server. Restoring data, for instance, involves retrieving data from a backup when local data has become corrupted or inaccessible.  

If you are using multiple Macs, as I do, and all Macs synchronize data to the same remote storage, there may be challenges maintaining synchronization
and preventing data loss, particularly if the remote storage is **not** a Git server, such as GitHub and Gitea. If the remote destinations are stored on a Git server, regular `git push` and `git pull` commands will suffice. 

Git is a superior tool for version control. However, in certain situations, creating a Git repository may not be feasible, and this function may prove useful. As a reminder, the Verify function is designed for multiple Macs synchronizing data to a single remote server as a backup. It also assists in deciding whether to push or pull changes to keep the local repository updated.

<div class="alert alert-danger" role="alert">

The user is solely responsible for determining the appropriate action. RsyncUI provides only advisory guidance, based on a rudimentary evaluation of a push and pull data comparison. Additionally, the function requires version 3.x of rsync to be installed and enabled.

The Verify process necessitates that one of the Macs be synchronized with the remote. If both Macs have local unique updates, the outcome of the Verify is most likely inaccurate, potentially resulting in data loss.

The function is not intended to be automated. Users must verify their subsequent actions. 

</div>

#### Synchronization of Multiple Macs to a Remote Server

I have over 3,000 bird photos (130 GB) from the past four years that are synchronized using RsyncUI to a local remote server at home. New photos are added, old photos are deleted, and updates are made to sidecars of the photos.  As long as I was using only one Mac, all updates were made on that Mac. However, with two Macs, I now use both Macs to work on my photos. When I synchronize my changes, I need to transfer those changes to my second Mac.

#### Arguments for rsync

The following arguments are used in both push and pull.

- `--itemize-changes` - output change-summary for all updates
- `--dry-run` - rsync execute an estimate run
- `--update` - evaluates the timestamp

The result from the `pull` command is subtracted from the result of the `push` command. Conversely, the `push` command is subtracted
from the result of the `pull` command. After both subtractions, the resulting arrays are compared based on the number of rows.

The outcome is as follows:

- If `pull` has more data than `push`, it is *likely* that the *destination* is more up-to-date than the *source*
- If `push` has more data than `pull`, it is *likely* that the *source* is more up-to-date than the *destination*
- If the number of rows is equal, it is *likely* that the *source* is more up-to-date than the *destination*

If there are zero rows, most likely, *source*  and *destination* are in sync. 

#### Itemized output - push or pull

The parameter `-i` or `--itemize-changes` produces details about each file. The format of the output is:

```bash
YXcstpoguax
|||||||||||
`-------------------------- the TYPE OF UPDATE:
 ||||||||||   <: file is being transferred to the remote host (pushed).
 ||||||||||   >: file is being transferred to the local host (pulled).
 ||||||||||   c: local change/creation for the item, such as:
 ||||||||||      - the creation of a directory
 ||||||||||      - the changing of a symlink,
 ||||||||||      - etc.
 ||||||||||   h: the item is a hard link to another item (requires --hard-links).
 ||||||||||   "+" - the file is newly created
 ||||||||||   .: the item is not being updated (though it might have attributes that are being modified).
 ||||||||||   *: means that the rest of the itemized-output area contains a message (e.g. "deleting").
 ||||||||||
 `----------------------------- the FILE TYPE:
  |||||||||   f for a file,
  |||||||||   d for a directory,
  |||||||||   L for a symlink,
  |||||||||   D for a device,
  |||||||||   S for a special file (e.g. named sockets and fifos).
  |||||||||
  `--------- c: different checksum (for regular files)
   ||||||||     CHANGED VALUE (for symlink, device, and special file)
   `-------- s: Size is different
    `------- t: Modification time is different
     `------ p: Permission are different
      `----- o: Owner is different
       `---- g: Group is different
        `--- u: The u slot is reserved for future use.
         `-- a: The ACL information changed
```
