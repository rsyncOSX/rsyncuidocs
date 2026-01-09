+++
author = "Thomas Evensen"
title = "Version 2.8.6"
date = "2026-01-09"
tags = ["changelog","version 2.8.6"]
categories = ["changelog"]
+++

### Version 2.8.6 - Jan 9, 2026

This release is a maintenance update.

There are a few UI updates.

The [Verify remote](https://rsyncui.netlify.app/docs/advanced/verify/) functionality has been removed and will be integrated into its own application. This change will enhance RsyncUI's focus on its core functionality, which is data synchronization.

For further details, please refer to the following documents:

- a detailed [Changelog](https://github.com/rsyncOSX/RsyncUI/blob/main/CHANGELOG.md)
- a [Code Quality Report](https://github.com/rsyncOSX/RsyncUI/blob/main/QUALITY_ANALYSIS_DETAILED.md)

<div class="alert alert-danger" role="alert">

The "missing stats alert" continues to occasionally appear. The package responsible for controlling the rsync process has been updated in development to resolve this issue. While I am aware of the cause of the problem, finding a solution that does not require setting a dedicated wait time appears to be somewhat challenging. However, I am actively working on this matter. To be released in next version.

</div>

### Empty stats file (no stats)

The process termination signal indicates that the external rsync process has completed and the process has been terminated. All tasks within the main synchronize view are updated with the latest run, but there is also a separate logging that records the main result of each task with a timestamp.

Occasionally, when synchronizing a small amount of data, the termination signal is detected before all output from rsync has been drained. In such cases, the separate logging may be missing. The process termination signal serves as a message to perform logging, but if the last summarized rsync output is missing, there is nothing to log. 

*Output from rsync* refers to the information that rsync provides to the terminal during the execution of a task.

<div class="alert alert-danger" role="alert">

If RsyncUI detects an empty statistics file, it will append a default log record stating `0 files : 0.00 MB in 0.00 seconds`.

</div>

If logging fails due to the aforementioned reason, this error will be generated, if *enabled*.

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}
