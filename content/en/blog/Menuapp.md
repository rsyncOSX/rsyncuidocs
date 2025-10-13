+++
author = "Thomas Evensen"
title = "RsyncUI menu app"
date = "2025-10-09"
tags = ["changelog","menuapp"]
categories = ["changelog"]
+++

### RsyncUI menu app - not yet released

*The primary objective of this application is to remain on the menu bar and provide effortless access to data synchronization.* 

{{% pageinfo color="info" %}}

The codebase has been streamlined, and all *model* and *process* code is shared with RsyncUI. The core code, model, and process code of the application have been validated through RsyncUI. I intend to continue updating the application until I believe it is ready for beta testing. After the beta release, I will evaluate the number of users to determine the next steps.

{{< /pageinfo >}}

Development efforts have primarily focused on the user interface. To the best of my ability, I have utilized the periphery tool to eliminate unused code. Additionally, there have been modifications to views to enhance their suitability for a menu bar application and minimize the memory footprint.

The following functions are **not available** in the menu application:

- there is no administrative task management
	- new tasks and profiles will be added by RsyncUI.
- there is no log views, logs may be viewed by RsyncUI
	- but logs are created by the menu app when executing tasks
- there is no support for URL commands
	- in RsyncUI URL commands are used to group together actions like estimate and execute tasks in one go 	 
- there is no restore of data
	- restore of data function is only valid for remote servers
- there is no Quick function

#### Number of lines of code

The RsyncUI menu application encompasses less than 50% of the code compared to RsyncUI.

```
cloc DecodeEncodeGeneric/Sources ParseRsyncOutput/Sources RsyncArguments/Sources RsyncUImenu/RsyncUImenu
      96 text files.
      95 unique files.                              
       4 files ignored.

github.com/AlDanial/cloc v 2.06  T=0.03 s (3329.6 files/s, 330155.3 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Swift                           89            977           1288           6741
C                                2             36             72            254
XML                              2              0              0             42
JSON                             1              0              0              6
C/C++ Header                     1              1              3              0
-------------------------------------------------------------------------------
SUM:                            95           1014           1363           7043
-------------------------------------------------------------------------------
```