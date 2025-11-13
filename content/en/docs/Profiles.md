+++
author = "Thomas Evensen"
date = "2024-03-11"
title =  "Profiles"
tags = ["profile"]
categories = ["synchronize"]
lastmod = "2024-03-18"
+++

Tasks can be organized in profiles. A profile is a named directory where RsyncUI stores its files. 

When you create a profile (for example, `newprofile`), RsyncUI creates a new directory at:
```
$HOME/.rsyncosx/<macserialnumber>/newprofile
```

where `<macserialnumber>` is your Mac's serial number. All tasks and log files for that profile are stored within this directory.

The list on the right side of the view displays all tasks that have not been updated within the number of days specified in the Settings under the "Mark days after" option.