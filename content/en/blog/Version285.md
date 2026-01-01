+++
author = "Thomas Evensen"
title = "Version 2.8.5"
date = "2026-01-01"
tags = ["changelog","version 2.8.5"]
categories = ["changelog"]
+++

### Version 2.8.5 - Jan 1, 2026

The release candidate is the "one table" version described below.

<div class="alert alert-danger" role="alert">

Add Tasks, Update Tasks, and Add Parameters now live in the main Tasks sidebar. To add a task, use the "+" button on the toolbar. This release brings many adjustments; expect additional small updates, bug fixes, and follow-up QA.

The following items are missing in this release candidate and will be added soon:

- validation of SSH parameters within the Parameter view, in code now (not rc)
- a view for displaying the complete rsync command, in code now (not rc)
- Enable full log of output from rsync to file, not part of settings, only valid for current run, to be implemented

Please test the release candidate and report bugs or feedback via email or GitHub Issues. The table and Inspectors may still change places; I am testing the best layout.

</div>

The main change in this version is significant UI refinement inspired by feedback from GitHub user @timreichen (Tim Reichen). Thank you for the suggestions.

The UI improvements utilize the Inspector view to provide detailed information about tasks. Adding new tasks is now facilitated through a dedicated sheet. 

### One table

In this version, only the Inspectors are present on each tabview. I personally find this version to be the most intuitive.

{{< figure src="/images/v285/one.png" alt="" position="center" style="border-radius: 8px;" >}}

### Two tables

The tables are duplicated within each tabview. 

{{< figure src="/images/v285/two.png" alt="" position="center" style="border-radius: 8px;" >}}
