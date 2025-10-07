+++
author = "Thomas Evensen"
title = "RsyncUI menu app"
date = "2025-10-07"
tags = ["changelog","menuapp"]
categories = ["changelog"]
+++

### RsyncUI menu app

I have commenced the development of a menu bar version of RsyncUI. *The primary objective of this application is to remain on the menu bar and provide effortless access to data synchronization.* 

**Not yet released as beta**. The core code, model, and process code of the application have been validated through RsyncUI. Development efforts have primarily focused on the user interface, and additional testing is required before the release of a beta version.

To the best of my ability, I have utilized the periphery tool to eliminate unused code. Additionally, there have been modifications to views to enhance their suitability for a menu bar application and minimize the memory footprint. Tables and data lists are converted to Lists, which, in my opinion, appear more visually appealing on a menu bar application. The codebase has been minimized, and all *model* and *process* code is shared with RsyncUI. 

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

#### The main menu and about

Upon clicking the menu bar icon for the application, the main view is displayed. Users can estimate and execute tasks, select tasks, double-click on tasks, and monitor the progress bar during task synchronization.

The primary view is independent of the menu bar, but clicking on the icon within the menu bar will either hide or reveal the application.

{{< figure src="/images/menuapp/main.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/menuapp/about.png" alt="" position="center" style="border-radius: 8px;" >}}

Estimate and synchronize estimated.

{{< figure src="/images/menuapp/estimating.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/menuapp/estimated.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/menuapp/synchronize.png" alt="" position="center" style="border-radius: 8px;" >}}
