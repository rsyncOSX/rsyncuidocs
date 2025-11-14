+++
author = "Thomas Evensen"
title = "Version 2.7.7"
date = "2025-11-14"
tags = ["changelog","version 2.7.7"]
categories = ["changelog"]
+++

### Version 2.7.7 (build 168) - Release Candidate (RC3)

**Note:** I initially believed that the next release, version 2.7.7, would be a minor update. However, it appears to be a more significant release. This is most likely the last RC before the new release.

All changes in code since version 2.7.6 can be viewed [here](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.7.6). The release is scheduled for late November. I personally use this version daily and frequently compile new versions when there are code updates.

### Real-Time Output

Real-time output from rsync is now included. You can find it within the "hidden" menu, accessible using the shortcut `⌘S` to reveal concealed toolbar options. The real-time view captures all output from rsync as it happens. The capture requires some additional CPU when activated, and it is automatically enabled and disabled when opening and closing the view. Additionally, the captured output is stored in memory and is cleared when the view is closed or by using the Clear button.

The real-time output captures the rsync output by an actor without blocking the @MainActor and UI updates. However, the @Observable object monitoring updates is executed on the @MainActor and updates the real-time view.

{{< figure src="/images/v277/capture1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v277/capture2.png" alt="" position="center" style="border-radius: 8px;" >}}

### Schedules

A bug related to deleting schedules has been fixed, and upon request, the weekly schedule has been reinstated. Schedules can only be added for the current and the next month. This restriction is implemented to manage memory usage effectively, as every schedule includes the callback action, which is stored in memory. Schedules are automatically saved to a file and reloaded into memory upon startup.

### Charts

A bug in the charts has been fixed. The bug could cause RsyncUI to crash.

### Continue Concealing Distractions

I am currently working on concealing even more *distractions*, and the next one will be located on the main toolbar. By using the shortcut `⌘S` (for showing or hiding) or by accessing the Task main menu, the Charts and Quick task will be displayed. They are concealed by default. To reveal them, simply toggle the show or hide option using the shortcut.

{{< figure src="/images/v277/toolbar1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v277/toolbar2.png" alt="" position="center" style="border-radius: 8px;" >}}

### Internal Refactor

Two minor but crucial objects have been refactored as Swift Package Manager (SPM) packages. Refactoring to SPM isolates the code, making it easier to test. The two objects are responsible for executing tasks, such as the actual `rsync` command with arguments outside of RsyncUI. Both objects listen for output from the tasks and the termination signal. If they fail, RsyncUI also fails.

A significant modification introduced by using SPM is the relocation of any local calls within the object to the outside of the SPM. This is achieved through Dependency Injection (DI). The process object depends on calling other objects within RsyncUI, and these objects are subsequently fed into the process object.

### Swift Packages for RsyncUI

The two latest SPM packages are *RsyncProcess* and *ProcessCommand*.

#### Main Repository

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - the main repository for RsyncUI

#### Local RsyncUI Packages (by SPM)

SPM makes it easy to create local packages. Each package contains its own tests using Swift Testing, the new framework for creating tests.

- **RsyncArguments** (https://github.com/rsyncOSX/RsyncArguments) - Generate parameters for `rsync` based on configurations
- **sshCreateKey** (https://github.com/rsyncOSX/sshCreateKey) - Assist in creating an SSH identity file and key using RsyncUI
	- generate an RSA-based SSH key for default and user-defined keys, including the SSH port number
- **DecodeEncodeGeneric** (https://github.com/rsyncOSX/DecodeEncodeGeneric) - Generic code for decoding and encoding JSON data
- **ParseRsyncOutput** (https://github.com/rsyncOSX/ParseRsyncOutput) - Parse and extract numerical values from the output of `rsync`
	- this data is used to display details and log results for synchronized tasks
- **RsyncUIDeepLinks** (https://github.com/rsyncOSX/RsyncUIDeepLinks) - Parse and return valid URL deeplinks to execute tasks directly within RsyncUI
- **RsyncProcess** (https://github.com/rsyncOSX/RsyncProcess) - A minor package but a core function of RsyncUI
	- listens for output from the rsync process as well as termination signal
- **ProcessCommand** (https://github.com/rsyncOSX/ProcessCommand) - As above, but for commands other than rsync