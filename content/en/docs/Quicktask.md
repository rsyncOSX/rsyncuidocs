+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "Quicktask"
tags = ["quick task"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++

{{< alert >}}

The Quick task function in this release is not functioning as intended due to an oversight on my part. Although it is a minor function and only applicable to remote servers, if you occasionally utilize it, there is a newer version, version 2.6.5, available for download that addresses the issue. If you do not require the Quick task function, there is no need to download the updated version.

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
