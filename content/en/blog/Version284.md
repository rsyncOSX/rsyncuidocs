+++
author = "Thomas Evensen"
title = "Version 2.8.4"
date = "2025-12-26"
tags = ["changelog","version 2.8.4"]
categories = ["changelog"]
+++

### Version 2.8.4 - Dec 26, 2025

Version 2.8.4rc2 has been promoted to the new release; no additional builds were produced.

<div class="alert alert-secondary" role="alert">

Version 2.8.2 has an "empty stats file" issue (details at the end of this page). I believe the root cause is the use of `AsyncSequence`/`AsyncStream` in the legacy *RsyncProcess* code from 2.8.2. A recent experiment to try the same approach in the new *RsyncProcessStreaming* package reproduced the problem.

</div>

<div class="alert alert-danger" role="alert">
  
Version 2.8.4 ships the *RsyncProcessStreaming* package variant that avoids the "empty stats file" issue.

</div>

I do not yet know why `AsyncStream` misbehaves here. I plan to investigate and add a mechanism to pause the process and drain remaining data before termination.

### Empty stats file

The process termination signal indicates that the external rsync process has completed and the process has been terminated. All tasks within the main synchronize view are updated with the latest run, but there is also a separate logging that records the main result of each task with a timestamp.

Occasionally, when synchronizing a small amount of data, the termination signal is detected before all output from rsync has been drained. In such cases, the separate logging may be missing. The process termination signal serves as a message to perform logging, but if the last summarized rsync output is missing, there is nothing to log. 

*Output from rsync* refers to the information that rsync provides to the terminal during the execution of a task.

<div class="alert alert-danger" role="alert">

If RsyncUI detects an empty statistics file, it will append a default log record stating `0 files : 0.00 MB in 0.00 seconds`.

</div>

If logging fails due to the aforementioned reason, this error will be generated, if *enabled*.

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}

