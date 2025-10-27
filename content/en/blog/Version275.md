+++
author = "Thomas Evensen"
title = "Version 2.7.5"
date = "2025-10-27"
tags = ["changelog","version 2.7.5"]
categories = ["changelog"]
+++

### Version 2.7.5 (build 166) - 27 October, 2025 release candidate (RC)

I intend to refrain from releasing a new public version until sometime in first week of November 2025. However, I will release new RC versions when there are updates.

Almost every button is adapted to a GlossyButton style on macOS Tahoe. On *previous* macOS versions there is applied a `.buttonStyle(.borderedProminent)` which makes the buttons blue, please see below. I am not sure if I should keep this style or remove it. If there are any comments, please let me know.

I think the applied GlossyButton on macOS Tahoe is very nice. In my opinion it makes the views more pleasant. Below are four views, with and without the updated button style.

The functions *Schedule* and *Verify remote* have been moved from the main sidebar to the toolbar. This modification enhances the cleanliness of the main sidebar by consolidating major functions. Additionally, there is an update to the progress bar. To display and access the toolbar actions for the two above mentioned functions, they must be enabled through the RsyncUI settings.

The primary sidebar retains its context sensitivity, but its functionality is limited to the *Snapshots* and *Restore* options, which are specifically tailored to certain tasks. For comprehensive information regarding the context-sensitive sidebar menu, please refer to the section titled *Getting started*.

##### The main view

*Schedule* and *Verify remote* moved to the toolbar. 

{{< figure src="/images/v275/main.png" alt="" position="center" style="border-radius: 8px;" >}}

##### Glossy and not so glossy buttons side by side 

{{< figure src="/images/v275/schedgl.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/sched.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/remotegl.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/remote.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/taskgl.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/task.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/verifygl.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/verify.png" alt="" position="center" style="border-radius: 8px;" >}}

