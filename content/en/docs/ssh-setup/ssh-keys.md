+++
author = "Thomas Evensen"
date = "2025-02-03"
title = "SSH keys and passwordless login"
tags = ["passwordless","ssh-key","remote servers"]
categories = ["ssh setup"]
+++

To synchronize to a remote server, RsyncUI requires passwordless SSH key authentication. Password-based authentication is not supported. SSH keys are more secure than passwords and allow RsyncUI to run unattended tasks without prompting.

### Default SSH keys

If you use the standard RSA key location (`~/.ssh/id_rsa`) and the default port 22, no extra configuration is needed in RsyncUI. RsyncUI detects the key automatically and appends `-e ssh` to the rsync command to tunnel and encrypt the transfer.

### Custom SSH keys

If you prefer a non-default key location or a custom port, you must create the key pair manually and tell RsyncUI where to find it.

RsyncUI passes custom key settings to rsync as:
```bash
-e "ssh -i ~/.keypath/identityfile -p NN"
```

where:

- `-i ~/.keypath/identityfile` is the SSH keypath and identity file
- `-p NN` is the port number (default 22)

Custom keypaths must start with `~` followed by `/` and contain at least two forward slashes. RsyncUI validates this before saving.

For example, a custom keypath might look like:
```bash
~/.ssh_rsyncosx/rsyncosx
```

And the resulting rsync command RsyncUI builds would be:
```bash
/opt/homebrew/bin/rsync --archive --verbose --compress \
-e "ssh -i ~/.ssh_rsyncosx/rsyncosx -p 22" --stats \
/Users/thomas/Documents/ thomas@raspberrypi:/backups/Documents/
```

---

### Step-by-step: creating a custom SSH key pair

RsyncUI uses the standard tools `ssh-keygen` and `ssh-copy-id`. Run the following steps in Terminal.

<div class="alert alert-secondary" role="alert">

Custom SSH key pairs must follow the format `~/.ssh_keypath/identityfile`, and the SSH port must be an integer value. RsyncUI validates these settings before saving.

</div>

#### Step 1: Create the SSH directory
```bash
cd
mkdir .ssh_rsyncosx
```

#### Step 2: Generate the key pair
```bash
ssh-keygen -t rsa -N "" -f ~/.ssh_rsyncosx/rsyncosx
```

**Parameters explained:**
- `-t rsa` — creates an RSA key pair
- `-N ""` — sets no passphrase
- `-f ~/.ssh_rsyncosx/rsyncosx` — specifies where to save the keys

#### Step 3: Copy the public key to the remote server
```bash
ssh-copy-id -i ~/.ssh_rsyncosx/rsyncosx.pub -p NN user@server
```

Replace `NN` with your SSH port (default 22), `user` with your remote username, and `server` with your server address.

#### Step 4: Set correct permissions
```bash
chmod 700 ~/.ssh_rsyncosx
```

#### Step 5: Verify the connection
```bash
/usr/bin/ssh -p NN -i ~/.ssh_rsyncosx/rsyncosx user@server
```

A successful login confirms the key pair is working. If it fails, check that `ssh-copy-id` completed without errors and that the permissions on `~/.ssh_rsyncosx` are correct.

#### Step 6: Configure RsyncUI

Open **Settings → SSH** and enter your custom keypath and identity file. RsyncUI will apply these settings to all remote tasks. You can also set per-task SSH parameters in the task's Parameters tab, which will override the global setting.
