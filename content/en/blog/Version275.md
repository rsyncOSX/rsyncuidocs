+++
author = "Thomas Evensen"
title = "Version 2.7.5"
date = "2025-10-25"
tags = ["changelog","version 2.7.5"]
categories = ["changelog"]
+++

### Version 2.7.5 (build 166) - 25 October, 2025 release candidate (RC)

I intend to refrain from releasing a new public version until sometime in November 2025. However, I will release new RC versions when there are updates.

Currently, there have been only a few UI updates. The graphical user interface (GUI) updates require a period of time to mature before they are finalized. The functions *Schedule* and *Verify remote* have been moved from the main sidebar to the toolbar. This modification enhances the cleanliness of the main sidebar by consolidating major functions. Additionally, there is an update to the progress bar.

Additionally, I have initiated the process of incorporating macOS Tahoe-specific features into certain views. Whenever a macOS Tahoe-specific feature is introduced, a `if #available(macOS 26.0, *) {...} else {...}` clause is employed to ensure that RsyncUI remains available for the most recent three major versions of macOS.

To display and access the toolbar actions for the two above mentioned functions, they must be enabled through the RsyncUI settings.

{{< figure src="/images/v275/main.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/schedule.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v275/verify.png" alt="" position="center" style="border-radius: 8px;" >}}

The progress bar has undergone a minor enhancement.

{{< figure src="/images/v275/progressview.png" alt="" position="center" style="border-radius: 8px;" >}}


