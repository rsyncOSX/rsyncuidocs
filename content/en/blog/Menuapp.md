+++
author = "Thomas Evensen"
title = "RsyncUI menu app"
date = "2025-10-09"
tags = ["changelog","menuapp"]
categories = ["changelog"]
+++

### RsyncUI menu app

The beta version is released for test. *The primary objective of this application is to remain on the menu bar and provide effortless access to data synchronization.*  As for RsyncUI the RsyncUI menu app is signed and notarized.

{{% pageinfo color="info" %}}

The codebase has been minimized, and all *model* and *process* code is shared with RsyncUI. The core code, model, and process code of the application have been validated through RsyncUI. 

{{< /pageinfo >}}

Development efforts have primarily focused on the user interface. To the best of my ability, I have utilized the periphery tool to eliminate unused code. Additionally, there have been modifications to views to enhance their suitability for a menu bar application and minimize the memory footprint. Tables and data lists are converted to Lists, which, in my opinion, appear more visually appealing on a menu bar application. 

#### Functions not within the menu app

The following functions is *not* within the menu app:

- there is no administrative task management
	- new tasks and profiles will be added by RsyncUI.
- there is no log views, logs may be viewed by RsyncUI
	- logs are created by the menu app
- there is no support for URL commands
- there is no restore of data
	- restore of data function is only valid for remote servers
- there is no Quick function

#### The main menu

Upon clicking the menu bar icon for the application, the main view is displayed. Users can estimate and execute tasks, select tasks, double-click on tasks, and monitor the progress bar during task synchronization.

The primary view is independent of the menu bar, but clicking on the icon within the menu bar will either hide or reveal the application.

{{< figure src="/images/menuapp/main.png" alt="" position="center" style="border-radius: 8px;" >}}

Estimate and synchronize estimated.

{{< figure src="/images/menuapp/estimating.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/menuapp/estimated.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/menuapp/synchronize.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Number of lines of code

RsyncUI comprises 191 files and 16,200 lines of code. The RsyncUI menu application encompasses less than 50% of the code compared to RsyncUI.

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