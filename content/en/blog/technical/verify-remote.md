+++
author = "Thomas Evensen"
title = "Verify remote"
date = "2025-10-27"
tags = ["verify remote"]
categories = ["technical details"]
+++

### Overview

<div class="alert alert-danger" role="alert">

This function has been removed from RsyncUI version 2.8.6 (January 8, 2026).

Currently, the function is being developed as a standalone application. Its continued use is essential, and it is preferable to use it independently rather than as a component of RsyncUI.

Utilizing the rsync parameter `--itemize-changes` will result in increased output from rsync. This parameter instructs rsync to generate a summary of changes for each file or directory it processes.

</div>

### Synchronization of Multiple Macs to a Remote Server

I have over 3,000 bird photos (130 GB) from the past four years that are synchronized using RsyncUI to a local remote server at home. New photos are added, old photos are deleted, and updates are made to photo sidecars. As long as I was using only one Mac, all updates were made on that Mac. However, with two Macs, I now use both to work on my photos. When I synchronize my changes, I need to transfer those changes to my second Mac.

### My Setup for securing bird photos

I back up my bird photography to multiple locations:

- a Raspberry Pi 5 server configured with two WD Red SA500 2.5" SSD 1TB drives set up as a mirrored ZFS pool
- a remote cloud service (JottaCloud)
- two 1TB NVMe external SSD drives attached to my computers

Typically, a synchronization action operates in a *one-way* direction. Local data is synchronized to backup media, such as an attached disk or a remote server. Restoring data, for instance, involves retrieving data from a backup when local data has become corrupted or inaccessible.  

If you are using multiple Macs, as I do, and all Macs synchronize data to the same remote storage, there may be challenges maintaining synchronization
and preventing data loss, particularly if the remote storage is **not** a Git server, such as GitHub and Gitea. If the remote destinations are stored on a Git server, regular `git push` and `git pull` commands will suffice. 

Git is a superior tool for version control. However, in certain situations, creating a Git repository may not be feasible, and this function may prove useful. As a reminder, the Verify function is designed for multiple Macs synchronizing data to a single remote server as a backup. It also assists in deciding whether to push or pull changes to keep the local repository updated.

<div class="alert alert-danger" role="alert">

The user is solely responsible for determining the appropriate action. RsyncUI provides only advisory guidance, based on a rudimentary evaluation of a push and pull data comparison. Additionally, the function requires version 3.x of rsync to be installed and enabled.

The Verify process necessitates that one of the Macs be synchronized with the remote. If both Macs have local unique updates, the outcome of the Verify is most likely inaccurate, potentially resulting in data loss.

The function is not intended to be automated. Users must verify their subsequent actions. 

</div>

### Arguments for rsync

The following arguments are used in both push and pull.

- `--itemize-changes` - output change-summary for all updates
- `--dry-run` - rsync execute an estimate run
- `--update` - evaluates the timestamp

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
```
Position  Letter  Meaning
--------  ------  ----------------------------------
    1       Y     Update type (<, >, c, h, ., *)
    2       X     File type (f, d, L, D, S)
    3       c     Checksum/content
    4       s     Size
    5       t     Time (modification)
    6       p     Permissions
    7       o     Owner
    8       g     Group
    9       u     Reserved/user time
   10       a     ACL
   11       x     Extended attributes

Special:  '.' = unchanged, '+' = new item
```

### The Stand alone application

<div class="alert alert-danger" role="alert">

Utilize RsyncUI to create tasks. The application necessitates RsyncUI for task creation and the activation of version 3.x of rsync. Furthermore, it is imperative that you thoroughly review the introductory section of this blog post, which elucidates the application's usage. I exclusively employ this application for synchronizing my bird photographs.

</div>

This application is currently in development. The majority of the code is derived from the code base of RsyncUI, and there are some new code modules associated with the Verify Remote function. Additionally, some new views have been added for evaluation purposes.

{{< figure src="/images/verifyremote/main.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/verifyremote/tagged.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/verifyremote/notag.png" alt="" position="center" style="border-radius: 8px;" >}}

## Overview

The `--itemize-changes` (or `-i`) option in rsync provides a detailed, itemized list of changes being made to each file during synchronization. The output format is an 11-character string followed by the file path. 

### Position 1: Update Type (Y)

The first character indicates the type of update operation. 

| Character | Meaning | Description |
|-----------|---------|-------------|
| `<` | Sent | File is being transferred to the remote host (sent) |
| `>` | Received | File is being transferred to the local host (received) |
| `c` | Local change | Local change/creation occurring (e.g., creating a directory, changing a symlink) |
| `h` | Hard link | Item is a hard link to another item (requires `--hard-links` option) |
| `.` | Not updated | Item is not being updated (though attributes may be modified) |
| `*` | Message | Rest of line contains a message (e.g., "deleting") |

---

### Position 2: File Type (X)

The second character indicates what type of filesystem object is being updated.

| Character | Type | Description |
|-----------|------|-------------|
| `f` | File | Regular file |
| `d` | Directory | Directory |
| `L` | Symlink | Symbolic link |
| `D` | Device | Device file |
| `S` | Special | Special file (e.g., named sockets, fifos) |

---

### Position 3: Checksum/Content (c)

| Character | Meaning | Context |
|-----------|---------|---------|
| `c` | Changed | Checksum differs (regular files) OR changed value (symlinks, devices, special files) |
| `+` | New | New item being created |
| `.` | Unchanged | No change to content/checksum |
| ` ` (space) | Same | Content is the same |

---

### Position 4: Size (s)

| Character | Meaning |
|-----------|---------|
| `s` | Size differs from source |
| `+` | New item |
| `.` | Size unchanged |

---

### Position 5:  Modification Time (t)

| Character | Meaning |
|-----------|---------|
| `t` | Modification time is different (lowercase) |
| `T` | Modification time is different (uppercase variant) |
| `+` | New item |
| `.` | Time unchanged |

---

### Position 6: Permissions (p)

| Character | Meaning |
|-----------|---------|
| `p` | Permissions are different |
| `+` | New item |
| `.` | Permissions unchanged |

---

### Position 7: Owner (o)

| Character | Meaning |
|-----------|---------|
| `o` | Owner is different |
| `+` | New item |
| `.` | Owner unchanged |

---

### Position 8: Group (g)

| Character | Meaning |
|-----------|---------|
| `g` | Group is different |
| `+` | New item |
| `.` | Group unchanged |

---

### Position 9: User/Reserved (u)

| Character | Meaning |
|-----------|---------|
| `u` | Reserved for future use (may indicate access time or creation time in some rsync versions) |
| `+` | New item |
| `.` | Unchanged |

**Note:** This position is reserved and its behavior may vary between rsync versions.

---

### Position 10: ACL (a)

| Character | Meaning |
|-----------|---------|
| `a` | ACL (Access Control List) information changed |
| `+` | New item with ACL |
| `.` | ACL unchanged |

**Note:** Requires ACL support to be compiled into rsync.

---

### Position 11: Extended Attributes (x)

| Character | Meaning |
|-----------|---------|
| `x` | Extended attribute (xattr) information changed |
| `+` | New item with extended attributes |
| `.` | Extended attributes unchanged |

**Note:** Requires extended attribute support to be compiled into rsync.

---

## Common Examples

### New Files

```
>f+++++++++ documents/report.pdf
```
- `>` = Receiving from remote
- `f` = Regular file
- `+++++++++` = All attributes are new (new file)

### Updated File

```
>f. st.. .... images/photo.jpg
```
- `>` = Receiving from remote
- `f` = Regular file
- `s` = Size changed
- `t` = Modification time changed
- Other attributes unchanged

### Directory Timestamp Change

```
.d..t...... src/components/
```
- `.` = Not being transferred (no update)
- `d` = Directory
- `t` = Modification time changed
- Other attributes unchanged

### Permission Change

```
.f... p. .... scripts/deploy.sh
```
- `.` = Not being transferred
- `f` = Regular file
- `p` = Permissions changed (e.g., made executable)
- Other attributes unchanged

### New Directory

```
cd+++++++++ backup/2024/
```
- `c` = Local creation
- `d` = Directory
- `+++++++++` = All attributes are new

### Symlink Changes

```
cLc.t...... config/current -> v2.0
```
- `c` = Local change
- `L` = Symlink
- `c` = Target/value changed (position 3)
- `t` = Modification time changed
- Other attributes unchanged

### Hard Link

```
hf...... .... docs/readme.txt => docs/README.txt
```
- `h` = Hard link
- `f` = File
- Other positions indicate which attributes differ between the link and its target

### Deletion

```
*deleting   old/obsolete.txt
```
- `*` = Special message
- Message indicates file is being deleted

### File Being Sent

```
<f. st...... data/export.csv
```
- `<` = Sending to remote
- `f` = Regular file
- `s` = Size differs
- `t` = Time differs

### Complex Example:  Multiple Changes

```
>f.stpog...  /var/www/index.html
```
- `>` = Receiving file
- `f` = Regular file
- `s` = Size changed
- `t` = Modification time changed
- `p` = Permissions changed
- `o` = Owner changed
- `g` = Group changed

## Version Differences

### rsync 3.0.9+ (Modern)
- Uses 11 characters:  `YXcstpoguax`
- Includes ACL (`a`) and extended attributes (`x`)

### rsync 2.6.8 and earlier (Legacy)
- Uses 9 characters: `YXcstpogz`
- No ACL or extended attribute indicators
- Position 9 was `z` (related to compression)



