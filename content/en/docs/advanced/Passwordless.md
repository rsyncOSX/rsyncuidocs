+++
author = "Thomas Evensen"
date = "2025-02-03"
title = "Passwordless login"
tags = ["passwordless","ssh-key", "remote servers"]
categories = ["advanced features"]
+++

To synchronize to a remote server using RsyncUI, passwordless SSH key authentication is required. RsyncUI does not support password-based authentication. SSH keys are generally more secure than passwords.

If *default values* for RSA-based SSH keys are used, no additional SSH info is needed in RsyncUI. Custom SSH keypaths, identity files, or port numbers must be configured.

The SSH keypath and identity file are specified as follows:
```bash
-e "ssh -i ~/.keypath/identityfile -p NN"
```

where:

- `-i ~/.keypath/identityfile` is the SSH keypath and identity file
- `-p NN` is the port number used for communication (default port 22)

To use custom SSH key and keypath data, add the following information to RsyncUI in the settings:

{{< figure src="/images/usersettings/ssh.png" alt="" position="center" style="border-radius: 8px;" >}}

To configure the SSH keypath and identity file, refer to the user configuration in the SSH settings. When enabling a custom SSH keypath and identity file, ensure they follow this format:
```bash
~/.mynewsshdirectory/mynewkey
```

For example:
```bash
~/.ssh_rsyncosx/rsyncosx
```

The path must start with `~` followed by `/`. RsyncUI will verify that the SSH keypath begins with `~` and contains at least two forward slashes (`/`) before saving the new SSH keypath.

The rsync command to synchronize my Documents directory to my Raspberry Pi server is set by RsyncUI as:
```bash
/opt/homebrew/bin/rsync --archive --verbose --compress \
-e "ssh -i ~/.ssh_rsyncosx/rsyncosx -p 22" --stats \
/Users/thomas/Documents/ thomas@raspberrypi:/backups/Documents/
```

For more information on passwordless login, please refer to the *Tools for passwordless login* section.