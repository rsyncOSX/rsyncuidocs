+++
author = "Thomas Evensen"
title = "Version 2.8.0"
date = "2025-12-01"
tags = ["changelog","version 2.8.0"]
categories = ["changelog"]
+++

### Version 2.8.0 (build 171) - not yet released

**Update: December 1, 2025**

The release candidate is not updated, but there have been more updates in the code *after the v2.7.9rc2 release*. However, the v2.7.9rc2 utilizes the most important part to test, which are all new updates to Swift Packages.

Here are all details about the [changed files](https://github.com/rsyncOSX/RsyncUI/compare/v2.7.8…main) since release *version 2.7.8*. The main GitHub repository is updated to version 2.8.0, and a new release is planned for some days. The following now summarizes all changes compared to the last release version 2.7.8:

- The major update within this release is that all seven Swift Packages (SPM) are updated to version 2.0.
  - All SPM are validated by their own test, using the new Swift Testing library.
- Several cleanups and refactorings have been made in the code.
  - There are approximately 17,300 lines of code, and some code has not been reviewed for some time.
    - It has been about five years since I commenced development of RsyncUI, based on code end experience from my previous project.
    - I have learned a lot during these years, and now most of the code has been reviewed at least once since the start of development.
    - Almost every time I review old code, there are some refactorings, simplifications, and cleaning of the code.
- A bug in the restore data functionality has been resolved.
- Only one Widget is now available, Estimate and Execute.
- All synchronization, such as quicktask and restore, now includes a progress bar if there has been an estimate ahead.
- Real-time capture of rsync includes capturing to a file. Users can view either the RsyncUI logfile or the rsync capture to file in the view logfile.
- A gesture has been added to indicate when buttons are pressed.

<div class="alert alert-secondary" role="alert">

Please be aware that real-time logging to file and view incurs a performance penalty. In certain instances, the termination signal may precede the complete draining of input from the filehandle, resulting in the absence of data for logging. While data synchronization is ensured, there may be no logging regarding the synchronization process.

My recommendation is to utilize this feature exclusively during the testing of new tasks and `—dry-run` tasks.

This feature is automatically disabled when the view is closed or switched off by buttons in the view.

</div>


<div class="alert alert-secondary" role="alert">

Regarding logging, a *previous bug* occurred when the termination signal was detected. This signal indicates that the external rsync process has completed and the process has been terminated. However, before all output from the process was captured, this could cause a crash of RsyncUI. All tasks within the main synchronize view are updated with the latest run, but there is also a separate logging that records the main result of each task with a timestamp.

Occasionally, when synchronizing data to fast SSDs, the termination signal is detected before all data has been received. While RsyncUI does not crash, the separate logging may be missing. After data synchronization and you don’t see a log, you can verify the synchronization of data by making a new estimate. The termination signal also serves as a message to perform logging, but if the last summarized rsync data is missing, there is nothing to log. 

Normally, the logging works as expected.

</div>

### Swift Packages

All SPM packages include their own testing mechanisms, and all tests have been successfully passed. SPM packages are generally small and focused on a specific purpose, which simplifies testing for edge cases and typical usage scenarios.

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
