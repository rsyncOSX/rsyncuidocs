+++
author = "Thomas Evensen"
title = "Version 2.8.3"
date = "2025-12-18"
tags = ["changelog","version 2.8.3"]
categories = ["changelog"]
+++

### Version 2.8.3 (build 174) - not yet released

<div class="alert alert-secondary" role="alert">

The planned release of version 2.8.3 was initially scheduled for December. However, it is more probable that the release will be postponed until the completion of version 2.8.4. Should any issues be identified in the current release, a bug fix for version 2.8.3 will be released.

One discovery utilizing the new RsyncProcessStreaming appears to resolve the issue of missing statistics. This is also one benefit documented within the blog post titled “Streaming Rsync Process, section 2. Better Resource Management".

</div>

The ongoing work on linting issues has resulted in the resolution of only a few remaining issues. A user-selected verification mechanism for default parameters, such as `—delete`, has been implemented:
- If the `—delete` parameter is included in the task configuration, the verification checks its presence or absence based on the task configuration’s state, which specifies whether a delete operation is required.
- Other default validated parameters include `—archive`, `—compress`, and `—dry-run`.
  - The `—archive` parameter is always enabled.
  - The `—compress` parameter is only applicable for remote tasks.
  - If RsyncUI requests an estimate, the validation checks that the `—dry-run` parameter is included within the arguments.

The user can toggle validation on or off, with the default setting being on. This configuration will be saved to the user settings.

Additionally, unused properties have been removed from the task itself. The required parameters are automatically added by the SPM RsyncArguments.

### Version 2.8.4 - work in progress

All of the aforementioned features are also included in the branch for version 2.8.4. However, there is a significant refactor for version 2.8.4: the Swift Package Manager (SPM) for the rsync process has been refactored. The blog post titled “Streaming Rsync Process” outlines the key differences and the rationale behind the refactor.

Version 2.8.4 is scheduled for release sometime in January 2026.

##### Swift Packages used by RsyncUI

All SPM packages are refactored, updated, and checked into the main branch. RsyncUI is a depended on all packages, but the last one is not mandatory. SSH keys can be generated via command line.

- *RsyncProcessStreaming* (https://github.com/rsyncOSX/RsyncProcessStreaming) - A minor package but a core function of RsyncUI
	- listens for output from the rsync process as well as termination signal
- *ProcessCommand* (https://github.com/rsyncOSX/ProcessCommand) - As above, but for commands other than rsync
- *RsyncArguments* (https://github.com/rsyncOSX/RsyncArguments) - Generate parameters for `rsync` based on configurations
- *DecodeEncodeGeneric* (https://github.com/rsyncOSX/DecodeEncodeGeneric) - Generic code for decoding and encoding JSON data
- *ParseRsyncOutput* (https://github.com/rsyncOSX/ParseRsyncOutput) - Parse and extract numerical values from the output of `rsync`
	- this data is used to display details and log results for synchronized tasks
- *RsyncUIDeepLinks* (https://github.com/rsyncOSX/RsyncUIDeepLinks) - Parse and return valid URL deeplinks to execute tasks directly within RsyncUI
- *sshCreateKey* (https://github.com/rsyncOSX/sshCreateKey) - Assist in creating an SSH identity file and key using RsyncUI
	- generate an RSA-based SSH key for default and user-defined keys, including the SSH port number
