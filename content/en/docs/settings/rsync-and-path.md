+++
author = "Thomas Evensen"
date = "2025-02-06"
title =  "Rsync and path"
tags = ["rsync and path"]
categories = ["usersettings"]
+++

After changing a setting, you have to save the changes to keep it next time you use RsyncUI.

{{< figure src="/images/usersettings/settings.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Version rsync

It is recommended to install the latest version of `rsync`. RsyncUI provides direct path support for Homebrew on both Apple Silicon and Intel Macs. `RsyncUI` will determine the type of Mac you are using. The default path for Homebrew is:

- Intel-based Mac: `/usr/local/bin`
- Apple Silicon: `/opt/homebrew/bin`

#### Path rsync

The *snapshot* and *syncremote* features require the latest rsync. If an updated or new rsync is not installed by Homebrew, set the path manually.

- If `Rsync v3.x` is enabled, set the *optional path* if not installed by Homebrew.
- Any version of `rsync` will work, but only the default macOS versions and the latest rsync release have been tested
    - testing and verification ensure accurate parsing of rsync output

#### Path for restore

- Preset temporary path for restoring single files and directory
- Preset temporary path for a full restore

#### Mark days after

Tasks with an execution date older than the number of days are marked red.

#### Backup configurations

You can back up the current setup, configurations, and logs (including all profiles) at any time by clicking the `wrench` button. The backup is copied to your Documents directory with a timestamp: `-month-day-year/hour/minute`.

The backups are located in your Documents directory: `$HOME/Documents/RsyncUIcopy-05-06-2024/08/21`
