+++
author = "Thomas Evensen"
title = "Number of files"
date = "2025-10-08"
tags = ["number of files"]
categories = ["technical details"]
+++

Numbers updated: October 8, 2025, version 2.7.3

There is a very nice and excellent tool, cloc (https://github.com/AlDanial/cloc), for counting of files and lines of code. Below are the numbers for Swift files which are part of the repository for compiling RsyncUI. RsyncUI does not rely on external libraries; it is constructed using default Swift libraries and Swift/SwiftUI code exclusively.

```
cloc DecodeEncodeGeneric/Sources ParseRsyncOutput/Sources RsyncArguments/Sources RsyncUI/RsyncUI RsyncUIDeepLinks/Sources SSHCreateKey/Sources
     192 text files.
     191 unique files.                                          
      10 files ignored.

github.com/AlDanial/cloc v 2.06  T=0.06 s (3305.4 files/s, 360653.0 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Swift                          185           2162           2351          15902
C                                2             36             72            254
XML                              2              0              0             53
JSON                             1              0              0              6
C/C++ Header                     1              1              3              0
-------------------------------------------------------------------------------
SUM:                           191           2199           2426          16215
-------------------------------------------------------------------------------
```

**Main Repository:**

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - The primary repository for RsyncUI.

**Local RsyncUI packages:**

SPM, Swift Package Manager, makes it easy to create local packages. And each package containes their own tests by Swift Testing, the new framwork for creating tests. All packages are created by me.

- RsyncArguments (https://github.com/rsyncOSX/RsyncArguments) - Generate parameters for `rsync` based on configurations.
- sshCreateKey (https://github.com/rsyncOSX/sshCreateKey) - Assist in creating an SSH identity file and key using RsyncUI.
	- Generate an RSA-based SSH key for default and user-defined keys, including the SSH port number.
- DecodeEncodeGeneric (https://github.com/rsyncOSX/DecodeEncodeGeneric) - Generic code for decoding and encoding JSON data.
- ParseRsyncOutput (https://github.com/rsyncOSX/ParseRsyncOutput) - Parse and extract numerical values from the output of `rsync`. This data is used to display details and log results for synchronized tasks.
- RsyncUIDeepLinks (https://github.com/rsyncOSX/RsyncUIDeepLinks) - parse end return valid URL deeplink for execute tasks direct within RsyncUI
