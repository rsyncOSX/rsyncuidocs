+++
author = "Thomas Evensen"
title = "Number of files"
date = "2025-02-01"
tags = ["number of files"]
categories = ["technical details"]
+++

Numbers updated: May 14, 2025, version 2.5.3

There is a very nice and excellent tool, cloc (https://github.com/AlDanial/cloc), for counting of files and lines of code. Below are the numbers for Swift files which are part of the repository for compiling RsyncUI. RsyncUI does not rely on external libraries; it is constructed using default Swift libraries and Swift/SwiftUI code exclusively.

```
cloc DecodeEncodeGeneric ParseRsyncOutput RsyncArguments RsyncUI RsyncUIDeepLinks SSHCreateKey
          313 text files.
     280 unique files.                                          
      61 files ignored.

github.com/AlDanial/cloc v 2.04  T=0.10 s (2797.8 files/s, 460541.4 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Text                             6             12              0          21921
Swift                          229           2351           2683          17792
XML                             24              0              0            582
C                                2             36             72            254
JSON                             8              0              0            204
make                             1             22              2             59
Markdown                         6             33              0             48
YAML                             2              0              0             12
Bourne Shell                     1              0              1              2
C/C++ Header                     1              1              3              0
-------------------------------------------------------------------------------
SUM:                           280           2455           2761          40874
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
