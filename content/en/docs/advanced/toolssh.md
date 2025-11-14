+++
author = "Thomas Evensen"
date = "2025-02-02"
title = "Tools for passwordless login"
tags = ["passwordless","ssh-key", "tools","remote servers"]
categories = ["advanced features"]
+++

RsyncUI uses the standard SSH tools `ssh-keygen` and `ssh-copy-id` to help you establish passwordless login to remote servers via SSH key authentication.

{{< alert >}}

Custom SSH key pairs must follow the format `~/.ssh_keypath/identityfile`, and the SSH port must be an integer value. RsyncUI validates these settings before saving.

{{< /alert >}}

## SSH Key Methods

RsyncUI supports two approaches:

1. **Default SSH keys**: Uses the standard RSA key location (`~/.ssh/id_rsa`)
2. **Custom SSH keys**: Uses a user-specified location (e.g., `~/.ssh_rsyncosx/rsyncosx`)

When using default keys, RsyncUI doesn't add extra SSH parameters to rsync commands. Custom keys require additional parameters to tell rsync where to find them.

## Step-by-Step: Creating Custom SSH Keys

### Step 1: Create the SSH Directory
```bash
cd
mkdir .ssh_rsyncosx
```

### Step 2: Generate the Key Pair
```bash
ssh-keygen -t rsa -N "" -f ~/.ssh_rsyncosx/rsyncosx
```

**Parameters explained:**
- `-t rsa` - Creates an RSA-based key pair
- `-N ""` - Sets no password (empty passphrase)
- `-f ~/.ssh_rsyncosx/rsyncosx` - Specifies where to save the keys

### Step 3: Copy Public Key to Server
```bash
ssh-copy-id -i ~/.ssh_rsyncosx/rsyncosx.pub -p NN user@server
```

Replace:
- `NN` with your SSH port number (default is 22)
- `user` with your remote username
- `server` with your server address

### Step 4: Set Correct Permissions
```bash
chmod 700 ~/.ssh_rsyncosx
```

### Step 5: Configure RsyncUI

Add your custom SSH keypath and identity file in RsyncUI's user configuration. RsyncUI will automatically apply these settings.

You can also set custom SSH parameters for individual tasks, which will override the global settings.