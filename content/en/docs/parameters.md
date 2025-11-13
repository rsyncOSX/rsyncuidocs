+++
author = "Thomas Evensen"
date = "2025-01-30"
title =  "Parameters to rsync"
tags = ["parameters"]
categories = ["rsync parameters"]
+++

RsyncUI provides default parameters for data synchronization. However, the actual default parameters utilized in tasks are determined by whether the rsync operation is performed over a network connection or to a local attached disk.

Users have the ability to modify default parameters as necessary. Parameters to rsync are stored in tasks, including a local ssh parameter if set. The local ssh parameter overrides a global ssh parameter if set.

{{< alert color="warning" >}}

Always verify the result of changing parameters to rsync before executing. Select *"Verify tasks"* from the primary Sidebar menu.

{{< /alert >}}

### Task-Specific Parameters to rsync

To add a parameter to rsync, enter it in the corresponding field. RsyncUI supports seven user-defined parameters. Users can add parameters using any of the fields. However, users are responsible for verifying the accuracy of the added parameters. If an incorrect parameter is added, rsync will generate an error message.

{{< figure src="/images/rsyncparameters/parameters.png" alt="" position="center" style="border-radius: 8px;" >}}

Parameters to rsync are typically constructed as follows. The following are examples only; `rsync` supports many parameters.

- parameter=value
	- `--exclude-from=/Volumes/home/user/exclude-list.txt` - exclude list for rsync
- parameters only
    - `--stats` - enables the display of statistics during the synchronization process
    - `--dry-run` - executes a simulated synchronization without modifying the files

For a comprehensive list of parameters for `rsync`, please refer to the official rsync documentation.

### Task-Specific SSH Parameter 

If default ssh-key values are used and no ssh-key information is provided in RsyncUI, the parameter `-e ssh` is appended to the rsync command to ensure data is tunneled and encrypted using ssh. This applies exclusively to remote servers and data restoration from remote servers.

Task-specific ssh parameters override global ssh parameters configured in the user settings.

- ssh-port: specify if ssh uses a port other than the default port 22
- ssh-keypath and identity file: typically, these are `.ssh/id_rsa`; set only if alternative ssh-keypath and identity file are to be used by ssh

{{< alert >}}

The values are marked red until validated OK. Refer to the *"Tools passwordless login"* section for information about validated values.

{{< /alert >}}

### Backup Switch

The `rsync` command allows you to instruct it to save modified and deleted files in a separate backup directory prior to the synchronization process. This feature can be enabled by setting the following parameters:

- `--backup` - Enables the saving of modified files
- `--backup-dir` - Specifies the directory where modified or deleted files should be saved before synchronization

RsyncUI provides a default value for this parameter, but you can customize it as needed. For a synchronized directory named `<directory to synchronize>`, the default backup directory is `../backup_<directory to synchronize>`, which is relative to the synchronized directory.