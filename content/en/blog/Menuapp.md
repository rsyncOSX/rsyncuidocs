+++
author = "Thomas Evensen"
title = "RsyncUI menu bar"
date = "2025-10-01"
tags = ["changelog","menuapp"]
categories = ["changelog"]
+++

### RsyncUI menu bar app

**Not yet released as alpha**. I am uncertain about the exact release date, but if you are interested in testing the app, please contact me via email.

I have commenced the development of a menu bar version of RsyncUI. The primary objective of this application is to remain on the menu bar and provide effortless access to data synchronization. 

There is no administrative task management. New tasks and profiles will be added by RsyncUI. There is no log views. Logs may be viewed by RsyncUI.

The codebase has been minimized, and all model and process code is shared with RsyncUI. Tables and data lists are converted to Lists, which, in my opinion, appear more visually appealing on a menu bar application.

To the best of my ability, I have utilized the periphery tool to eliminate unused code. Additionally, there have been modifications to views to enhance their suitability for a menu bar application and minimize the memory footprint.

#### The main menu and about

Upon clicking the menu bar icon for the application, the main view is displayed. Users can estimate and execute tasks, select tasks, double-click on tasks, and monitor the progress bar during task synchronization.

{{< figure src="/images/menuapp/main.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/menuapp/about.png" alt="" position="center" style="border-radius: 8px;" >}}

Estimate and synchronize estimated.

{{< figure src="/images/menuapp/estimated.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/menuapp/synchronize.png" alt="" position="center" style="border-radius: 8px;" >}}
