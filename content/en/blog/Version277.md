+++
author = "Thomas Evensen"
title = "Version 2.7.7"
date = "2025-11-07"
tags = ["changelog","version 2.7.7"]
categories = ["changelog"]
+++

### Version 2.7.7 (build 168) - not yet released

*There will be a rc in a few days.* All changes in code since version 2.7.6 can be viewed [here](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.7.6) - xxx commits to main since this release. 

The release is scheduled for late November or early December. I personally utilize this version daily and frequently compile new versions when there are code updates. Additionally, I employ AI tools such as Claude Code and GitHub Copilot to assist me in coding. While these tools are valuable resources, they occasionally encounter challenges in producing code that functions as intended. 

The development of the next version has commenced. While there are no new features yet, the internal code is undergoing refactoring. Two minor, but crucial objects are being refactored as Swift Package Manager (SPM) objects. Refactoring to SPM isolates the code, making it easier to test. The two final objects to be refactored are responsible for executing tasks, such as the actual `rsync` command with arguments outside of RsyncUI. Both objects listen for output from the tasks and the termination signal. If they fail, RsyncUI also fails.

### Continue hide distractions

I am currently working on concealing distractions, and the next one will be located on the main toolbar. By utilizing the shortcut `⌘S` (for displaying or concealing) or by accessing the Task main menu, the Charts and Quick task will be presented. It is concealed by default. To reveal it, simply toggle the show or hide option using the shortcut.

{{< figure src="/images/v277/toolbar1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v277/toolbar2.png" alt="" position="center" style="border-radius: 8px;" >}}

### Internal refactor

A few internal refactors have been implemented. One notable refactor involves converting critical code to Swift Package Manager (SPM). This refactor offers several significant benefits, including the isolation and utilization of Swift Testing for testing the isolated code. Additionally, there are other refactors and ideas that have emerged from reading blogs about Swift, which I follow. 

### Bugs

I have also fixed a bug in the Charts. The bug may cause RsyncUI to crash. 

### Swift Packages

The two last SPM are *RsyncProcess* and *ProcessCommand*. The test cases for the last two SPM are in development.

#### Main Repository

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - the main repository for RsyncUI

#### Local RsyncUI packages (by SPM)

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
