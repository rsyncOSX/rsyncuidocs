+++
author = "Thomas Evensen"
date = "2025-01-30"
title =  "RsyncUI files, JSON"
tags = ["files", "JSON"]
categories = ["general information"]
+++

RsyncUI stores all its data locally on your Mac in [JSON](https://en.wikipedia.org/wiki/JSON) format. This includes task configurations, log records, and user settings. Understanding the file structure can be helpful for backup or troubleshooting purposes.

## File Locations

All RsyncUI files are stored in: `$HOME/.rsyncosx/<macserialnumber>`, where `<macserialnumber>` is your Mac's serial number. RsyncUI retrieves this serial number automatically at startup.

At startup, RsyncUI reads the user settings and default configuration from JSON files. Log records are only loaded when viewing logs or when updating logs after a synchronization task.

### Configuration Files

Task configurations are stored in:

`$HOME/.rsyncosx/<macserialnumber>/configurations.json`

If you use profiles, each profile has its own configuration file:

`$HOME/.rsyncosx/<macserialnumber>/<profile>/configurations.json`

### Log Records

Synchronization logs are stored in:

`$HOME/.rsyncosx/<macserialnumber>/<profile>/logrecords.json`

### User Settings

User settings are stored in:

`$HOME/.rsyncosx/<macserialnumber>/rsyncuiconfig.json`

User settings apply to all profiles.

### The Log File

The application log file is a text file that can be viewed within RsyncUI:

`$HOME/.rsyncosx/<macserialnumber>/rsyncui.txt`