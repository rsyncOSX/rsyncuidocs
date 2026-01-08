+++
author = "Thomas Evensen"
title = "Verify remote"
date = "2025-02-05"
tags = ["verify remote","synchronize"]
categories = ["advanced features"]
+++

<div class="alert alert-danger" role="alert">

This function has been removed from RsyncUI version 2.8.6  (January 8, 2026). It will be developed as a standalone application and may delete data if used improperly.

The Verify remote function is disabled by default. See *RsyncUI settings, Log settings* to enable. This function requires the destination to be on a remote server.

</div>

<div class="alert alert-danger" role="alert">

Prior to utilizing this function, kindly consult its documentation to ensure you make the appropriate decision.

The Verify remote function helps synchronize multiple Macs to a single remote repository (excluding Git repositories) and update local data from the same remote.

This was built for a personal need. I use two Macs for photo development and synchronize data to a remote folder. The remote is not a Git repository, so a tool was needed to decide whether to push or pull data.

Important: This method requires you to remember which Mac last synced. If not, you risk data loss. Establish a procedure. For example, at home I always use my Mac Mini M4 to edit photos. When traveling, I always use my MacBook Pro, fully synced with my Mac Mini before I leave.

</div>

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
