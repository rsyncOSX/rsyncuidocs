+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "Quicktask"
tags = ["quick task"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++

{{< alert >}}

The Quick task function in version 2.6.4 is not working as it should, my fault. It is a minor function and only valid for remote servers. But if you sometimes use it, there is a new version 2.6.5 for download which fixes the issue. If you don’t need Quick task, don’t bother to download.

{{< /alert >}}

Use QuickTask for quickly copy or transfer files to either source or destination. QuickTask will save the last executed quick task as default values. Default values can be cleared by the toolbar function.

There are two types of quick tasks:

- *synchronize* - synchronize local files to remote, aka *push* data
- *syncremote* - synchronize remote files to local, aka *pull* data

Trailing /

- *Add trailing slash* - add a trailing slash to both the source and destination
- *Do not add trailing slash* - do not add a trailing slash, or if added, remove it
- *Do not check* - do not check for trailing slash or not on either the source or destination

{{< figure src="/images/quicktask/quicktask.png" alt="" position="center" style="border-radius: 8px;" >}}

After entering data, the default task is a `--dry-run` task. It is recommended to inspect the result before executing the actual run.

#### Folder parameters

- *Source folder* - required field
- *Destination folder* - required field
  - a `~` is expanded as the home directory with the full path by the remote operating system
  - the remote directory may also be specified by full path, depending on where the backup directory is located on the remote server

#### Remote parameters

- *Remote username* -  username for login to the remote server
- *Remote server* - either server name or IP address for the remote server
