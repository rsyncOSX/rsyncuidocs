+++
author = "Thomas Evensen"
title = "Version 2.8.5"
date = "2025-12-31"
tags = ["changelog","version 2.8.5"]
categories = ["changelog"]
+++

### Version 2.8.5 - In development

<div class="alert alert-danger" role="alert">
  
This version introduces several modifications. Additionally, I anticipate the implementation of minor updates and bug fixes, as well as a quality assurance and review process of changes. A release candidate is scheduled for early January 2026, followed by a final release in January 2026.

I have encountered an unforeseen issue that renders RsyncUI unresponsive. The cause of this issue remains unknown, and I require some time to investigate further. The issue manifests when attempting to close the Inspector in the Parameters view. Upon doing so, RsyncUI becomes unresponsive, displaying a "bounching beach ball" and force quit RsyncUI is requiered.

The positive news is that I have likely identified the code responsible for the issue.

</div>

The primary advancement in this version is the implementation of significant user interface (UI) enhancements. These updates were requested by GitHub user @timreichen (Tim Reichen) to enhance the intuitiveness of RsyncUI. Tim Reichen's input is greatly appreciated.

The UI improvements utilize the Inspector view to provide detailed information about tasks. Adding new tasks is now facilitated through a dedicated sheet. Selecting a task displays its associated details. Additionally, a toggle on the toolbar allows users to switch between viewing task data and parameters.

The detail views are implemented by utilizing SwiftUI Inspector view.

{{< figure src="/images/v285/nr1.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v285/nr2.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v285/nr3.png" alt="" position="center" style="border-radius: 8px;" >}}

