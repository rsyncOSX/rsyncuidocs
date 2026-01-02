+++
author = "Thomas Evensen"
title = "Version 2.8.5"
date = "2026-01-02"
tags = ["changelog","version 2.8.5"]
categories = ["changelog"]
+++

### Version 2.8.5 - Jan 2, 2026 (updated)

Release Candidate 2 introduces a new feature in the user settings, allowing users to select between two versions of Inspector views (as detailed below). A restart of RsyncUI is necessary for the changes to take effect. Additionally, validation of SSH parameters has been incorporated. 

The main change in this version is significant UI refinement inspired by feedback from GitHub user @timreichen (Tim Reichen). Thank you for the suggestions. The UI improvements utilize the Inspector view to provide detailed information about tasks. Adding new tasks is now facilitated through a dedicated sheet. 

<div class="alert alert-danger" role="alert">

Add Tasks, Update Tasks, and Add Parameters now live in the main Tasks sidebar. To add a task, use the "+" button on the toolbar. This release brings many adjustments; expect additional small updates, bug fixes, and follow-up QA.

The following function is missing in this release candidate and will be added before release:

- enable full log of output from rsync to file, not part of settings, only valid for current run, to be implemented

Please test the release candidate and report bugs or feedback via email or GitHub Issues. The table and Inspectors may still change places; I am testing the best layout.

</div>

### What are the main difference

The “one table” Inspector utilizes a single table for both Tasks and Parameters, and the Inspector is presented within each tab. In contrast, the “two table” version employs two tables, each tab presenting a table and Inspector when selected. This version provides more space for the Inspector.

### Add and Edit tasks

{{< figure src="/images/v285/one1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v285/two1.png" alt="" position="center" style="border-radius: 8px;" >}}

### Add and Edit parameters for rsync

{{< figure src="/images/v285/one2.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v285/two2.png" alt="" position="center" style="border-radius: 8px;" >}}
