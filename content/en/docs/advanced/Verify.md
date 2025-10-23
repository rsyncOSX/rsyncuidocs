+++
author = "Thomas Evensen"
title = "Verify remote"
date = "2025-02-05"
tags = ["verify remote","synchronize"]
categories = ["advanced features"]
+++

{{< alert >}}

 The Verify remote function is by default disabled. Please refer to section *RsyncUI settings, Monitor and log* to enable.

{{< /alert >}}

{{< alert color="warning" >}}

The Verify remote function is not enabled by default. To enable it, please navigate to Settings and toggle the corresponding option. Before utilizing this function, kindly refer to its documentation to ensure you make the appropriate decision.  

The Verify remote function is a specialized tool designed when synchronizing two Mac computers to a single repository, excluding Git repositories. This functionality was developed by the developer due to a personal need. The developer utilizes two Macs for photo development and data synchronization to a remote folder. The remote repository is not a Git server, necessitating a tool to determine whether to push or pull data.

{{< /alert >}}

Typically, a synchronize action operates in a *one-way* direction of data. Local data is synchronized to a backup media, such as an attached disc or a remote server. Restoring data, for instance, involves retrieving data from a backup when local data has become corrupted or inaccessible.  

If you are using multiple Macs, as I do, and all Macs synchronize data to the same remote storage, there may be challenges maintaining synchronization
and preventing data loss, particularly if the remote storage is **not** a Git server, such as GitHub and Gitea. If the remote destinations are stored on a Git server, regular `git push` and `pull` commands will suffice. 

Git is a superior tool for version control. However, in certain situations, creating a Git repository may not be feasible, and this function may prove useful. As a reminder, the Verify function is designed for multiple Macs synchronizing data to a single remote server as a backup. It also assists in deciding whether to push or pull changes to keep the local repository updated.

The verification applies only to remote destinations on servers

{{< alert color="warning" >}}

The user is solely responsible for determining the appropriate action. RsyncUI provides only advisory guidance, based on a rudimentary evaluation of a push and pull data comparison. Additionally, the function requires version 3.x of rsync to be installed and enabled.

The Verify process necessitates that one of the Macs be synchronized with the remote. If both Macs have local unique updates, the outcome of the Verify is most likely inaccurate, potentially resulting in data loss.

The function is not intended to be automated. Users must verify their subsequent actions. 

{{< /alert >}}

#### Synchronization of Multiple Macs to a Remote Server

I have over 3,000 bird photos (130 GB) from the past four years that are synchronized using RsyncUI to a local remote server at home.
New photos are added, old photos are deleted, and updates are made to sidecars of the photos.  As long as I was using only one Mac,
all updates were made on that Mac. However, with two Macs, I now use both Macs to work on my photos.
When I synchronize my changes, I need to transfer those changes to my second Mac.

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

{{% pageinfo color="info" %}}

I utilize this function on a regular basis. I frequently travel to my mountain cabin, capture photographs of the wildlife, and develop images on my MacBook Pro during my stays. At home, I primarily use my MacMini 4 with a large monitor. Subsequently, I employ this function to synchronize my Macs with the photographs. As usual, I recall which Mac is most current. Occasionally, both the pull and push view contain data after a dry run, making it challenging to determine the appropriate course of action. I do recall which Mac is most current and include the delete parameter to synchronize. However, without remembering which Mac is most updated, it may be difficult to determine the correct action.

Therefore, my advice is to ensure that you are aware of which Mac is updated. Furthermore, avoid making changes on both Macs and synchronizing changes to the repository, as this may result in data loss. 

{{< /pageinfo >}}

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
