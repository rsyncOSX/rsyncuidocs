+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "Restore data"
tags = ["restore"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++

Data restoration from within RsyncUI is only available for remote servers. For data stored on attached volumes, use macOS Finder to restore files. A restore operation must be executed to a temporary restore path to prevent overwriting your original data.

### How to Restore Files

1. **Filter files**: Use the filter field to search for specific files or directories. The filter retrieves only filenames containing the specified string.

{{< figure src="/images/restore/restore_filter_all.png" alt="" position="center" style="border-radius: 8px;" >}}

2. **Select files**: Choose either a file or a directory to restore.

3. **View the command**: Toggle the *command* switch to see the actual restore command that will be executed.

4. **Preview the restore**: Select *restore* to display a `--dry-run` preview of the restore operation.

{{< figure src="/images/restore/restore_filter.png" alt="" position="center" style="border-radius: 8px;" >}}

5. **Execute the restore**: Turn off the `--dry-run` toggle to perform the actual restore.

{{< figure src="/images/restore/restore_dryrun.png" alt="" position="center" style="border-radius: 8px;" >}}

6. **Review results**: After the restore completes, RsyncUI displays the output from rsync.