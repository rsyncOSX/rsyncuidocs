+++
author = "Thomas Evensen"
title = "Version 2.8.0"
date = "2025-12-02"
tags = ["changelog","version 2.8.0"]
categories = ["changelog"]
+++

### Version 2.8.0 (build 171) - Dec 2, 2025

*There is a new issue summarizing, by GitHub Copilot, all changes since version 2.7.8.*

The following summarizes changes in this release:

- The major update within this release is that all seven Swift Packages (SPM) are updated to version 2.0.
  - All SPM are validated by their own test, using the new Swift Testing framework.
- Several cleanups and refactorings have been made in the code.
  - There are approximately 17,000 lines of Swift code, and some code has not been reviewed for some time.
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

### No stats

*In the upcoming maintenance release, version 2.8.1, an alert will be introduced to notify users when RsyncUI detects a lack of data to write logdata. While still in development, RsyncUI in version 2.8.1 will now throw an error when this condition is met. Notably, the loop for executing and estimating will continue to run even after the error is encountered.*

<div class="alert alert-secondary" role="alert">

The process termination signal indicates that the external rsync process has completed and the process has been terminated. All tasks within the main synchronize view are updated with the latest run, but there is also a separate logging that records the main result of each task with a timestamp.

Occasionally, when synchronizing a small amount of data to fast SSDs, the termination signal is detected before all output from rsync has been received. In such cases, the separate logging may be missing. After data synchronization and the absence of a log, you can verify the synchronization of data by recalculating the estimate. 

The process termination signal serves as a message to perform logging, but if the last summarized rsync output is missing, there is nothing to log. 

*Output from rsync* refers to the information that rsync provides to the terminal during the execution of a task.

Normally, the logging works as expected.

</div>

In the upcoming version of RsyncUI, a new error will be introduced. If logging fails due to the aforementioned reason, this error will be generated. Notably, I am unable to produce this error when executing RsyncUI within Xcode. However, it is only when running RsyncUI as an application compiled for release that this error is encountered. Executing RsyncUI within Xcode results in increased code execution time, and the summarized output from rsync is captured when the termination signal is detected.

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}

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
