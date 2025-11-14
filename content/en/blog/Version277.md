+++
author = "Thomas Evensen"
title = "Version 2.7.7"
date = "2025-11-14"
tags = ["changelog","version 2.7.7"]
categories = ["changelog"]
+++

### Version 2.7.7 (build 168) - Release Candidate (RC3)

**Note:** I initially believed that the next release version 2.7.7, would be a minor update. However, it appears to be a more significant release. This is most likely the last rc before a new release.

All changes in code since version 2.7.6 can be viewed [here](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.7.6) - xxx commits. The release is scheduled for late November. I personally utilize this version daily and frequently compile new versions when there are code updates. 

### Real-time output

The real-time output from rsync is included. You will find it within the “hidden” menu, and you can access it by using the shortcut ⌘S to reveal concealed toolbar options. The real-time view captures all output from rsync in real-time. The capture requires some additional CPU when activated, and it is automatically enabled and disabled when opening and closing the view. Additionally, the captured output is stored in memory and is cleared when the view is closed or by using the Clear button.

{{< figure src="/images/v277/capture1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v277/capture2.png" alt="" position="center" style="border-radius: 8px;" >}}

### Schedules

A bug related to deleting schedules has been fixed, and upon request, the weekly schedule has been reinstated. Schedules will only be valid added for the current and the next month.This restriction is implemented to manage memory usage effectively, as every schedule includes the callback action, which is stored in memory. Schedules are automatically saved to a file and reloaded into memory upon startup.

### Charts

There is fixed a bug in the Charts. The bug may cause RsyncUI to crash. 

### Continue concealing distractions

I am currently working on concealing even more *distractions*, and the next one will be located on the main toolbar. By utilizing the shortcut `⌘S` (for displaying or concealing) or by accessing the Task main menu, the Charts and Quick task will be presented. It is concealed by default. To reveal it, simply toggle the show or hide option using the shortcut.

{{< figure src="/images/v277/toolbar1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v277/toolbar2.png" alt="" position="center" style="border-radius: 8px;" >}}


### Internal refactor

Two minor, but crucial objects has been refactored as Swift Package Manager (SPM) objects. Refactoring to SPM isolates the code, making it easier to test. The two objects are responsible for executing tasks, such as the actual `rsync` command with arguments outside of RsyncUI. Both objects listen for output from the tasks and the termination signal. If they fail, RsyncUI also fails. 

A significant modification introduced by utilizing SPM is the relocation of any local calls within the object to the outside of the SPM. This is achieved through the implementation of Dependency Injection (DI). The process object is dependent on calling other objects within RsyncUI, and these objects are subsequently fed into the process object.

### Swift Packages for RsyncUI

The two last SPM are *RsyncProcess* and *ProcessCommand*.

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
