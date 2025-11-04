+++
author = "Thomas Evensen"
title = "Version 2.7.7"
date = "2025-11-04"
tags = ["changelog","version 2.7.7"]
categories = ["changelog"]
+++

### Version 2.7.7 (build 168) - not yet released

The release is scheduled for late November or early December. I personally utilize this version daily and frequently compile new versions when there are code updates. Additionally, I employ AI tools such as Claude Code and GitHub Copilot to assist me in coding. While these tools are valuable resources, they occasionally encounter challenges in producing code that functions as intended. 

The development of the next version has commenced. While there are no new features yet, the internal code is undergoing refactoring. Two minor, but crucial objects are being refactored as Swift Package Manager (SPM) objects. Refactoring to SPM isolates the code, making it easier to test. The two final objects to be refactored are responsible for executing tasks, such as the actual `rsync` command with arguments outside of RsyncUI. Both objects listen for output from the tasks and the termination signal. If they fail, RsyncUI also fails.

The two last SPM are *RsyncProcess* and *ProcessCommand*. The test cases for the last two SPM are in development.

##### Main Repository

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - the main repository for RsyncUI

##### Local RsyncUI packages (by SPM)

SPM makes it easy to create local packages. And each package containes their own tests by Swift Testing, the new framwork for creating tests. All packages are created by me. 

- RsyncArguments (https://github.com/rsyncOSX/RsyncArguments) - Generate parameters for `rsync` based on configurations
- sshCreateKey (https://github.com/rsyncOSX/sshCreateKey) - Assist in creating an SSH identity file and key using RsyncUI
	- generate an RSA-based SSH key for default and user-defined keys, including the SSH port number
- DecodeEncodeGeneric (https://github.com/rsyncOSX/DecodeEncodeGeneric) - Generic code for decoding and encoding JSON data
- ParseRsyncOutput (https://github.com/rsyncOSX/ParseRsyncOutput) - Parse and extract numerical values from the output of `rsync`
	- this data is used to display details and log results for synchronized tasks
- RsyncUIDeepLinks (https://github.com/rsyncOSX/RsyncUIDeepLinks) - parse end return valid URL deeplink for execute tasks direct within RsyncUI
- RsyncProcess (https://github.com/rsyncOSX/RsyncProcess) - one minor package, but a core function of RsyncUI
	- listens for output from the rsync process as well as termination signal
- ProcessCommand (https://github.com/rsyncOSX/ProcessCommand) - as above, but for other commands than rsync

#### AI

I am actively collaborating with two AI services, Claude Code and GitHub Copilot, to identify potential improvements. Their suggestions are being evaluated, and I am testing their recommendations. While some suggestions prove effective, others require manual code adjustments. Each time a fix is implemented, the code undergoes a slight increase in complexity, which I sometimes find undesirable.

In summary, AI support in coding is highly beneficial and enjoyable. I utilize AI for minor code snippets and to identify the reasons behind code failures when they occur.