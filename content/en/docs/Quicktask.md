+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "QuickTask"
tags = ["quick task"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++

Utilize QuickTask to swiftly duplicate or transfer files between the source and destination. QuickTask will retain the most recently executed quick task as default settings. Default settings can be cleared through the toolbar function. QuickTask is exclusively applicable to remote servers and necessitates the activation of Passwordless login via SSH.

There are two types of quick tasks:

- *synchronize* - synchronize local files to remote, aka *push* data
- *syncremote* - synchronize remote files to local, aka *pull* data

### Trailing Slash Options

- *Add* - adds a trailing slash to both the source and destination
- *Do not add* - does not add a trailing slash, or if added, removes it
- *Do not check* - does not check for a trailing slash on either the source or destination

{{< figure src="/images/quicktask/quicktask.png" alt="" position="center" style="border-radius: 8px;" >}}

After entering data, the default task is a `--dry-run` task. It is recommended to inspect the result before executing the actual run.

### Folder Parameters

- *Source folder* - required field
- *Destination folder* - required field
  - a `~` is expanded as the home directory with the full path by the remote operating system
  - the remote directory may also be specified by full path, depending on where the backup directory is located on the remote server

### Remote Parameters

- *Remote username* - username for login to the remote server
- *Remote server* - either server name or IP address for the remote server