+++
author = "Thomas Evensen"
title = "Version 2.7.5"
date = "2025-10-28"
tags = ["changelog","version 2.7.5"]
categories = ["changelog"]
+++

### Version 2.7.5 (build 166) - 28 October, 2025

Changes in this release are, UI changes only:

Buttons on macOS Tahoe are adapted to the new Liquid Glass style. On *previous* macOS versions there is applied a `.buttonStyle(.borderedProminent)` which makes the buttons blue, please see below. I think the applied Liquid Glass style on macOS Tahoe is very nice. In my opinion it makes the views more pleasant. Below are four views, with and without the updated button style.

The functions *Schedule* and *Verify remote* have been moved from the main sidebar to the toolbar. This modification enhances the cleanliness of the main sidebar by consolidating major functions. Additionally, there is an update to the progress bar. To display and access the toolbar actions for the two above mentioned functions, they must be enabled through the RsyncUI settings.

The primary sidebar retains its context sensitivity, but its functionality is limited to the *Snapshots* and *Restore* options, which are specifically tailored to certain tasks. For comprehensive information regarding the context-sensitive sidebar menu, please refer to the section titled *Getting started*.

##### The main view

*Schedule* and *Verify remote* moved to the toolbar. 

{{< figure src="/images/v275/main.png" alt="" position="center" style="border-radius: 8px;" >}}

##### Liquid Glass style and default button style side by side 

{{< figure src="/images/v275/schedgl.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/verifygl.png" alt="" position="center" style="border-radius: 8px;" >}}


