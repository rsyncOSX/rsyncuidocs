+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "Quicktask"
tags = ["quick task"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++
{{< alert color="warning" >}}

Note: Be aware of if using syncremote, the *remote folder must be added first* and  the *local folder as second*. This is fixed in code which make RsyncUI to flip folders. To be released later as a maintenance release. This only apply to the quick task. 

There also seems to be an issue with GUI for selecting local folders. Please use drag and drop for local folders. The GUI for selecting folders are removed. To be released later as a maintenance release. This only apply to the quick task. 

{{< /alert >}}

Use QuickTask for quickly copy or transfer files to either local or remote storage. QuickTask will save the last executed quick task as default values. Default values can be cleared by the toolbar function.

There are two types of quick tasks:

- `synchronize`: synchronize local files to remote, aka *push* data
- `syncremote`: synchronize remote files to local, aka *pull* data

{{< figure src="/images/quicktask/quicktask.png" alt="" position="center" style="border-radius: 8px;" >}}

After entering data, the default task is a `--dry-run` task. It is recommended to inspect the result before executing the actual run.

#### Folder parameters

- **Local folder**: a required field
- **Remote folder**: a required field
  - a `~` is expanded as the home directory with the full path by the remote operating system
  - the remote directory may also be specified by full path, depending on where the backup directory is located on the remote server

#### Remote parameters

- **Remote username**: the username for logging into the remote server
- **Remote server**: either the server name or IP address for the remote server
