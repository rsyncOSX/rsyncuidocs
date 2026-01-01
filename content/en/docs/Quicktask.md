+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "QuickTask"
tags = ["quick task"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++

Use QuickTask to quickly copy or transfer files. QuickTask remembers the last task as defaults; you can clear them via the toolbar. QuickTask works only with remote servers and requires passwordless SSH login.

There are two types of quick tasks:

- *synchronize* - synchronize local files to remote, aka *push* data
- *syncremote* - synchronize remote files to local, aka *pull* data

### Trailing Slash Options

- *Add* - adds a trailing slash to both the source and destination
- *Do not add* - does not add a trailing slash, or if added, removes it
- *Do not check* - does not check for a trailing slash on either the source or destination

{{< figure src="/images/quicktask/quicktask.png" alt="" position="center" style="border-radius: 8px;" >}}

After entering data, the default task is a `--dry-run` task. Inspect the result before executing the actual run.

### Folder Parameters

- *Source folder* - required
- *Destination folder* - required
  - `~` expands to the remote home directory
  - you can also use the full path, depending on where the backup is stored on the remote

### Remote Parameters

- *Remote username* - username for login to the remote server
- *Remote server* - either server name or IP address for the remote server