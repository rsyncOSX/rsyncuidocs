+++
author = "Thomas Evensen"
title = "Version 2.7.7"
date = "2025-11-13"
tags = ["changelog","version 2.7.7"]
categories = ["changelog"]
+++

### Version 2.7.7 (build 168) - Release Candidate (RC2)

All changes in code since version 2.7.6 can be viewed [here](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.7.6) - xxx commits to main since this release.  The release is scheduled for late November. I personally utilize this version daily and frequently compile new versions when there are code updates. 

### Update Nov 13

An update to the rc has been released. A bug related to deleting schedules has been fixed, and upon request, the weekly schedule has been reinstated. However, it is important to note that I still need to conduct some quality assurance testing of the schedule function before a new release.

*In the current rc2 release, only schedules for the current month are permitted to be added. There are a few minor bugs in the schedule that have been fixed in the code but have not yet been released. In the next release, schedules will only be valid added for the current and the next month.This restriction is implemented to manage memory usage effectively, as every schedule includes the callback action, which is stored in memory. Schedules are automatically saved to a file and reloaded into memory upon startup. There is potential for refactoring the schedule in a future release.*

#### Capture output real-time

The forthcoming version of RsyncUI will incorporate real-time capture output from rsync. However, I must still include a user-defined option to enable or disable this feature due to the resource-intensive nature of capturing real-time output.

{{< figure src="/images/v277/capture.png" alt="" position="center" style="border-radius: 8px;" >}}

### Update Nov 12

As of now, there are no updates to the RC. However, I have made some further enhancements to the [RsyncProcess Swift Package](https://github.com/rsyncOSX/RsyncProcess). New within the package is the ability to read the output from the rsync process in real-time. Within the summarized view, you will receive the output from each task estimated, but this view is completed after the task is finished.

The real-time view of rsync output is not yet included in RsyncUI. However, there is a minor, menu-based version of RsyncUI called [RsyncUImenu](https://github.com/rsyncOSX/RsyncUImenu) that includes this feature. The model of the RsyncUImenu app is a clone of the model for RsyncUI. The only new development is the UI part. The RsyncUImenu app can be used in parallel with RsyncUI, but not simultaneously.

You may consider testing [RsyncUImenu](https://github.com/rsyncOSX/RsyncUImenu). It has been in development for some time and should be as stable as RsyncUI. Please note that it remains active in the menu bar until explicitly closed.

### Internal refactor

Two minor, but crucial objects has been refactored as Swift Package Manager (SPM) objects. Refactoring to SPM isolates the code, making it easier to test. The two objects are responsible for executing tasks, such as the actual `rsync` command with arguments outside of RsyncUI. Both objects listen for output from the tasks and the termination signal. If they fail, RsyncUI also fails. 

A significant modification introduced by utilizing SPM is the relocation of any local calls within the object to the outside of the SPM. This is achieved through the implementation of Dependency Injection (DI). The process object is dependent on calling other objects within RsyncUI, and these objects are subsequently fed into the process object. As an example:

```
let handlers = ProcessHandlers(
            processtermination: processtermination_estimation,
            filehandler: { _ in
                Logger.process.info("ProcessRsync: You should not SEE this message")
            },
            rsyncpath: GetfullpathforRsync().rsyncpath,
            checklineforerror: TrimOutputFromRsync().checkforrsyncerror,
            updateprocess: SharedReference.shared.updateprocess,
            propogateerror: { error in
                SharedReference.shared.errorobject?.alert(error: error)
            },
            logger: { command, output in
                _ = await ActorLogToFile(command, output)
            },
            checkforerrorinrsyncoutput: SharedReference.shared.checkforerrorinrsyncoutput,
            rsyncversion3: SharedReference.shared.rsyncversion3,
            environment: MyEnvironment()?.environment
        )
```

The actual definition of the ProcessHandlers is within the [SPM](https://github.com/rsyncOSX/RsyncProcess).

### Continue concealing distractions

I am currently working on concealing even more *distractions*, and the next one will be located on the main toolbar. By utilizing the shortcut `⌘S` (for displaying or concealing) or by accessing the Task main menu, the Charts and Quick task will be presented. It is concealed by default. To reveal it, simply toggle the show or hide option using the shortcut.

{{< figure src="/images/v277/toolbar1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v277/toolbar2.png" alt="" position="center" style="border-radius: 8px;" >}}

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
