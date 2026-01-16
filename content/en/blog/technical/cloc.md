+++
author = "Thomas Evensen"
title = "Number of files"
date = "2026-01-15"
tags = ["number of files"]
categories = ["technical details"]
+++

Numbers updated: January 15, 2026 (version 2.9.0).

RsyncUI depends only on the standard Swift and SwiftUI toolchain—no external libraries.

```
cloc DecodeEncodeGeneric/Sources ParseRsyncOutput/Sources RsyncArguments/Sources RsyncUI/RsyncUI RsyncUIDeepLinks/Sources SSHCreateKey/Sources RsyncProcessStreaming/Sources ProcessCommand/Sources RsyncAnalyse/Sources

     210 text files.
     209 unique files.                                          
      12 files ignored.

github.com/AlDanial/cloc v 2.06  T=0.07 s (3067.2 files/s, 358028.7 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Swift                          203           2824           2713          18434
C                                2             36             72            254
XML                              2              0              0             53
JSON                             1              0              0              6
C/C++ Header                     1              1              3              0
-------------------------------------------------------------------------------
SUM:                           209           2861           2788          18747
-------------------------------------------------------------------------------
```

#### Main Repository

- RsyncUI (https://github.com/rsyncOSX/RsyncUI) - the main repository for RsyncUI

##### Swift Packages used by RsyncUI

All SPM packages are refactored, updated, and tracked in the main branch. RsyncUI depends on all of them except the last, which is optional because SSH keys can be generated from the command line.

- *RsyncProcessStreaming* (https://github.com/rsyncOSX/RsyncProcessStreaming) - A core function of RsyncUI
	- listens for output from the rsync process as well as termination signal
- *ProcessCommand* (https://github.com/rsyncOSX/ProcessCommand) - As above, but for commands other than rsync
- *RsyncArguments* (https://github.com/rsyncOSX/RsyncArguments) - Generate parameters for `rsync` based on configurations
- *DecodeEncodeGeneric* (https://github.com/rsyncOSX/DecodeEncodeGeneric) - Generic code for decoding and encoding JSON data
- *ParseRsyncOutput* (https://github.com/rsyncOSX/ParseRsyncOutput) - Parse and extract numerical values from the output of `rsync`
	- this data is used to display details and log results for synchronized tasks
- *RsyncUIDeepLinks* (https://github.com/rsyncOSX/RsyncUIDeepLinks) - Parse and return valid URL deeplinks to execute tasks directly within RsyncUI
- *sshCreateKey* (https://github.com/rsyncOSX/sshCreateKey) - Assist in creating an SSH identity file and key using RsyncUI
	- generate an RSA-based SSH key for default and user-defined keys, including the SSH port number
