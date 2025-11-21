+++
author = "Thomas Evensen"
title = "Version 2.7.9"
date = "2025-11-21"
tags = ["changelog","version 2.7.9"]
categories = ["changelog"]
+++

### Version 2.7.9 (build 170) - in development and test

Currently, the sole modification between this version and version 2.7.8 is the utilization of the most recent refactored Swift Packages (SPM). It is important to note that this version is still under testing. All SPM packages include their own testing mechanisms, and all tests have been successfully passed. However, as always, a test is only as reliable as the methodology employed to develop it. Therefore, there may still be undiscovered bugs.

SPM packages are generally small and focused on a specific purpose, which simplifies testing for edge cases and typical usage scenarios. Nevertheless, it is crucial to remember that no code is entirely bug-free. 

#### Main Repository

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - the main repository for RsyncUI

#### Swift Packages used by RsyncUI

All SPM packages are refactored, updated, and checked into the main branch.

SPM simplifies the creation of local packages. Each package contains its own tests utilizing Swift Testing, the latest framework for test creation. RsyncUI is a dependency for all packages, but the last one is not mandatory. SSH keys can be generated via command line.

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
