+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "Profiles"
tags = ["profile"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++

Tasks can be organized into profiles. A profile is a named directory where RsyncUI stores its files.

When you create a profile (for example, `newprofile`), RsyncUI creates a new directory at:
```
$HOME/.rsyncosx/<macserialnumber>/newprofile
```

where `<macserialnumber>` is your Mac's serial number. All tasks and log files for that profile are stored within this directory.

### Why use profiles?

Profiles are useful for separating unrelated sets of tasks — for example, one profile for work backups and another for personal photos. Switching profiles loads only the tasks for that profile, keeping the task list focused.

### Creating and switching profiles

Open the profile picker from the toolbar or the File menu. Enter a name and confirm to create a new profile. Selecting an existing profile loads its tasks immediately.

### Stale task indicator

The list on the right shows tasks not updated within the number of days set under "Mark days after" in Settings. Tasks older than that threshold are highlighted in red as a reminder to run them.