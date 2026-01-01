+++
author = "Thomas Evensen"
title = "Version 2.8.5"
date = "2026-01-01"
tags = ["changelog","version 2.8.5"]
categories = ["changelog"]
+++

### Version 2.8.5 - Jan 1, 2026

The release candidate is the "one table version", see below. 

<div class="alert alert-danger" role="alert">

The Add tasks, Update tasks, and Add Parameters to task functionalities have been integrated into the main sidebar Tasks menu. To add a task, select the “+” button on the toolbar. This version introduces several modifications. Additionally, minor updates, bug fixes, and a quality assurance and review process of changes are anticipated.

The following features are missing within the release candidate and will be added soon:

1. Validation of SSH parameters within the Parameter view.
2. A view for displaying the complete rsync command.
3. Enable full log of output from rsync to file, not part of settings, only valid for current run.

Please test the release candidate and report any bugs or other comments via email or by adding an Issue. The table and Inspectors may be flipped, but I am uncertain about the optimal arrangement.


</div>

The primary advancement in this version is the implementation of significant user interface (UI) enhancements. These updates were requested by GitHub user @timreichen (Tim Reichen) to enhance the intuitiveness of RsyncUI. Tim Reichen's input is greatly appreciated. 

The UI improvements utilize the Inspector view to provide detailed information about tasks. Adding new tasks is now facilitated through a dedicated sheet. 

### One table

In this version, only the Inspectors are present on each tabview. I personally find this version to be the most intuitive.

{{< figure src="/images/v285/one.png" alt="" position="center" style="border-radius: 8px;" >}}

### Two tables

The tables are duplicated within each tabview. 

{{< figure src="/images/v285/two.png" alt="" position="center" style="border-radius: 8px;" >}}
