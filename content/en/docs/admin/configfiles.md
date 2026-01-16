+++
author = "Thomas Evensen"
date = "2025-01-30"
title =  "RsyncUI files, JSON"
tags = ["files", "JSON"]
categories = ["general information"]
+++

RsyncUI stores all data locally on your Mac in [JSON](https://en.wikipedia.org/wiki/JSON) format, including task configurations, logs, and settings. Understanding the file structure helps with backup and troubleshooting.

## File Locations

All RsyncUI files are stored in: `$HOME/.rsyncosx/<macserialnumber>`, where `<macserialnumber>` is your Mac's serial number, which is retrieved at startup.

At startup, RsyncUI reads user settings and the default configuration from JSON files. Log records load only when viewing or updating logs.

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