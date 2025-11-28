+++
author = "Thomas Evensen"
title = "Version 2.7.9"
date = "2025-11-27"
tags = ["changelog","version 2.7.9"]
categories = ["changelog"]
+++

### Version 2.7.9 (build 170) - November 27, 2025 release candidate

Scheduled for release in first week of December 2025.

The Full Changelog, in Release page, shows details about all changes.

The real-time capture of rsync includes capturing to a file. Users can view either the RsyncUI logfile or the rsync capture to file in the view logfile.

<div class="alert alert-secondary" role="alert">

Please be aware that real-time logging to file and view incurs a performance penalty. In certain instances, the termination signal may precede the complete draining of input from the filehandle, resulting in the absence of data for logging. While data synchronization is ensured, there may be no logging regarding the synchronization process.

My recommendation is to utilize this feature exclusively during the testing of new tasks and `—dry-run` tasks.

This feature is automatically disabled when the view is closed or switched off by buttons in the view.

</div>

Additionally, a gesture has been added to indicate when buttons are pressed.

And there are a few other internal refactors as well. 

The primary modification between this version and *version 2.7.8* (released version) is the utilization of the most recent refactored Swift Packages (SPM). All SPM packages include their own testing mechanisms, and all tests have been successfully passed. SPM packages are generally small and focused on a specific purpose, which simplifies testing for edge cases and typical usage scenarios.

#### Main Repository

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - the main repository for RsyncUI

#### Swift Packages used by RsyncUI

All SPM packages are refactored, updated, and checked into the main branch. RsyncUI is a depended on all packages, but the last one is not mandatory. SSH keys can be generated via command line.

- *RsyncProcess* (https://github.com/rsyncOSX/RsyncProcess) - A minor package but a core function of RsyncUI
	- listens for output from the rsync process as well as termination signal
- *ProcessCommand* (https://github.com/rsyncOSX/ProcessCommand) - As above, but for commands other than rsync
- *RsyncArguments* (https://github.com/rsyncOSX/RsyncArguments) - Generate parameters for `rsync` based on configurations
- *DecodeEncodeGeneric* (https://github.com/rsyncOSX/DecodeEncodeGeneric) - Generic code for decoding and encoding JSON data
- *ParseRsyncOutput* (https://github.com/rsyncOSX/ParseRsyncOutput) - Parse and extract numerical values from the output of `rsync`
	- this data is used to display details and log results for synchronized tasks
- *RsyncUIDeepLinks* (https://github.com/rsyncOSX/RsyncUIDeepLinks) - Parse and return valid URL deeplinks to execute tasks directly within RsyncUI
- *sshCreateKey* (https://github.com/rsyncOSX/sshCreateKey) - Assist in creating an SSH identity file and key using RsyncUI
	- generate an RSA-based SSH key for default and user-defined keys, including the SSH port number
