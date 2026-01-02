+++
author = "Thomas Evensen"
title = "Version 2.8.5"
date = "2026-01-02"
tags = ["changelog","version 2.8.5"]
categories = ["changelog"]
+++

### Version 2.8.5 - Jan 2, 2026

The release candidate is the "one table" version. The code has been updated to support both versions, and I need to determine how to switch between them. It is likely that this will be a user setting. Therefore, there is no longer a need to make a decision, as both versions are supported. 

<div class="alert alert-danger" role="alert">

Add Tasks, Update Tasks, and Add Parameters now live in the main Tasks sidebar. To add a task, use the "+" button on the toolbar. This release brings many adjustments; expect additional small updates, bug fixes, and follow-up QA.

The following items are missing in this release candidate and will be added soon:

- validation of SSH parameters within the Parameter view, in code now (not rc)
- a view for displaying the complete rsync command, in code now (not rc)
- enable full log of output from rsync to file, not part of settings, only valid for current run, to be implemented

Please test the release candidate and report bugs or feedback via email or GitHub Issues. The table and Inspectors may still change places; I am testing the best layout.

</div>

The main change in this version is significant UI refinement inspired by feedback from GitHub user @timreichen (Tim Reichen). Thank you for the suggestions. The UI improvements utilize the Inspector view to provide detailed information about tasks. Adding new tasks is now facilitated through a dedicated sheet. 

### What are the main difference

The “one table” Inspector utilizes a single table for both Tasks and Parameters, and the Inspector is presented within each tab. In contrast, the “two table” version employs two tables, each tab presenting a table and Inspector when selected. This version provides more space for the Inspector.

### Add and Edit tasks

{{< figure src="/images/v285/one1.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v285/two1.png" alt="" position="center" style="border-radius: 8px;" >}}

### Add and Edit parameters for rsync

{{< figure src="/images/v285/one2.png" alt="" position="center" style="border-radius: 8px;" >}}
{{< figure src="/images/v285/two2.png" alt="" position="center" style="border-radius: 8px;" >}}
