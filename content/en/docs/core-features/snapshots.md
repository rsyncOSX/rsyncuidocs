+++
author = "Thomas Evensen"
date = "2025-02-01"
title =  "Snapshots"
tags = ["snapshot"]
categories = ["advanced features"]
+++

<div class="alert alert-secondary" role="alert">

Snapshots are an effective way to restore previous data and deleted files. They use [hardlinks](https://en.wikipedia.org/wiki/Hard_link) to save copies of only modified and deleted files. Unchanged files remain as hardlinks to the original.

</div>

In each snapshot task, RsyncUI stores the next snapshot number. The number increments by one after each run. Rsync automatically creates the next snapshot directory, and RsyncUI updates the stored number. The number is displayed as part of the log timestamp.

If a file named "file.txt" is saved in the initial snapshot and remains unchanged or is deleted, the "file.txt" in the latest snapshot is a hardlink to the original file in the first snapshot.

If "file.txt" is deleted from the source, the filesystem manages the hardlink appropriately during the delete operation.

In RsyncUI, the first and last snapshots are never deleted, even if all snapshots are marked for deletion.

### Snapshots

A snapshot is a saved state or backup of data at a specific point in time. Each snapshot is synchronized with the source at the time of creation.

#### Remote Server

The rsync parameter for the next snapshot to synchronize to a *remote.server* is:
```
--link-dest=~/snapshots/n-1 /Users/thomas/data/ user@remote.server:~/snapshots/n
```

where:

- `n` is the number of the next snapshot to be synchronized
- `n-1` is the latest synchronized snapshot
- `/Users/thomas/data/` is *the source* directory, only read by rsync
- `~/snapshots/` is *the destination* directory where snapshots are synchronized

#### Local Attached Disk

The above example with a local attached disk, mounted at `/Volumes/backup`, is:
```
--link-dest=/Volumes/backup/snapshots/n-1 /Users/thomas/data/ /Volumes/backup/snapshots/n
```

where:

- `n` is the number of the next snapshot to be synchronized
- `n-1` is the latest synchronized snapshot
- `/Users/thomas/data/` is *the source* directory, only read by rsync
- `/Volumes/backup/snapshots/` is *the destination* directory where snapshots are synchronized

#### Snapshot Creation

To create a snapshot task, select "snapshot" as the action in the *Add tasks* section. RsyncUI automatically manages the snapshot number "n" for the task. This number represents the next available snapshot number and is used to calculate the rsync parameter.

#### Snapshot Administration

Snapshot administration is essential for maintaining an organized and efficient backup system. It involves regularly reviewing and deleting unnecessary or outdated snapshots to prevent clutter and optimize backup space usage.

#### Deleting Snapshots

Deleting snapshots is a destructive operation that should be performed with caution. It is important to have a plan in place to determine which snapshots to keep and which to delete. RsyncUI provides a simple plan for managing snapshot retention.

#### The Plan for Keep and Delete

Selecting the "Tag" button evaluates all snapshots based on the date within the log record. Based on the selected plan and date, snapshots are either tagged with "keep" or "delete." Snapshots tagged with "delete" are also preselected for deletion. To delete the marked snapshots, select the "Delete" button.

Even if all snapshots are tagged for deletion, the first and last snapshots are never deleted. They are automatically removed from the delete list during the internal preparation for deletion.

The plan is based on three time periods, where the `plan` parameter affects *previous months (and years)*:

- **The current week**
  - keep all snapshots within the current week
  - the value of `plan` has no effect on the current week
  
- **The current month** (minus the current week)
  - keep *all snapshots* for the selected day of week, e.g., all snapshots every Sunday this month
  - the value of `plan` has no effect on the current month
  
- **Previous months (and years)**
  - keep the snapshot in the last week of the month for the selected day of week, e.g., the last Sunday in the month
  - if `plan == Every`, keep snapshots for the selected day of week, e.g., all snapshots every Sunday in previous periods
  - if `plan == Last`, keep snapshots for the selected day of week, e.g., all snapshots on the last Sunday of every month in previous periods

#### Tagging and Deleting Snapshots

It is recommended to optimize the number of snapshots regularly. Select a plan, tag the snapshots, and delete the snapshots marked for deletion.