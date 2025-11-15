+++
author = "Thomas Evensen"
title = "Number of files"
date = "2025-10-17"
tags = ["number of files"]
categories = ["technical details"]
+++

Numbers updated: November 15, 2025, version 2.7.7 rc4

There is a very nice and excellent tool, [cloc](https://github.com/AlDanial/cloc), for counting of files and lines of code. Below are the numbers for Swift files which are part of the repository for compiling RsyncUI. RsyncUI does not rely on external libraries; it is constructed using default Swift libraries and Swift/SwiftUI code exclusively.

```
cloc RsyncUI/RsyncUI DecodeEncodeGeneric/Sources ParseRsyncOutput/Sources RsyncArguments/Sources  RsyncUIDeepLinks/Sources SSHCreateKey/Sources RsyncProcess/Sources ProcessCommand/Sources
     201 text files.
     201 unique files.                                          
       8 files ignored.

github.com/AlDanial/cloc v 2.06  T=0.06 s (3319.3 files/s, 371034.7 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Swift                          195           2324           2489          17230
C                                2             36             72            254
XML                              2              0              0             53
JSON                             1              0              0              6
C/C++ Header                     1              1              3              0
-------------------------------------------------------------------------------
SUM:                           201           2361           2564          17543
-------------------------------------------------------------------------------
```

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
