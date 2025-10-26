+++
author = "Thomas Evensen"
title = "Version 2.7.5"
date = "2025-10-26"
tags = ["changelog","version 2.7.5"]
categories = ["changelog"]
+++

### Version 2.7.5 (build 166) - 26 October, 2025 release candidate (RC)

Even more glassy buttons are added to code, and a few more to add as well. And the glassy buttonstyle is also tweaked a little bit. *A new rc with most buttons supporting glassy buttonstyle to be released in a day or two.* Below are views of the schedule modale view, with glossy buttons for macOS Tahoe and buttons for the two previous major versions of macOS. 

I intend to refrain from releasing a new public version until sometime in November 2025. However, I will release new RC versions when there are updates.

Currently, there have been only a few UI updates. The graphical user interface (GUI) updates require a period of time to mature before they are finalized. The functions *Schedule* and *Verify remote* have been moved from the main sidebar to the toolbar. This modification enhances the cleanliness of the main sidebar by consolidating major functions. Additionally, there is an update to the progress bar.

The primary sidebar retains its context sensitivity, but its functionality is limited to the *Snapshots* and *Restore* options, which are specifically tailored to certain tasks. For comprehensive information regarding the context-sensitive sidebar menu, please refer to the section titled *Getting started*.

Additionally, I have initiated the process of incorporating macOS Tahoe-specific features into certain views. Whenever a macOS Tahoe specific feature is introduced, a `if #available(macOS 26.0, *) {...} else {...}` compiler directive is employed to ensure that RsyncUI remains available for the most recent three major versions of macOS.

To display and access the toolbar actions for the two above mentioned functions, they must be enabled through the RsyncUI settings.

##### The main view

*Schedule* and *Verify remote* moved to the toolbar. 

{{< figure src="/images/v275/main.png" alt="" position="center" style="border-radius: 8px;" >}}

##### Glossy buttons

For macOS Tahoe.

{{< figure src="/images/v275/glossybuttons.png" alt="" position="center" style="border-radius: 8px;" >}}

##### Not glossy Buttons

For macOS Sonoma and macOS Sequoia.

{{< figure src="/images/v275/buttons.png" alt="" position="center" style="border-radius: 8px;" >}}



