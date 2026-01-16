+++
author = "Thomas Evensen"
title =  "Synchronize data"
date = "2025-02-10"
tags = ["synchronize"]
categories = ["synchronize"]
+++

<div class="alert alert-secondary" role="alert">

The *Synchronize* view runs all or selected tasks in a single operation via *shortcut actions* or toolbar *functions*.

For a single task, the first double-click initiates a `--dry-run` estimate; a second double-click executes the actual run.

</div>

Shortcut actions within the *Synchronize* view:

- *estimate* - shortcut `⌘E` estimates all or selected tasks
- *synchronize* - shortcut `⌘R` synchronizes all or selected tasks without estimation
  - no progress bar during synchronization; a progress bar requires estimation first
- *abort* - shortcut `⌘K` aborts and halts any ongoing task

RsyncUI opens the *Synchronize* view at launch. Click the *wand and stars* (shortcut `⌘E`) on the toolbar to estimate all tasks.

{{< figure src="/images/tasks/tasks.png" alt="" position="center" style="border-radius: 8px;" >}}

The estimate displays with blue numbers indicating data to be synchronized. To synchronize from the summarized estimate view, press the left arrow (shortcut `⌘R`) on the toolbar.

By selecting a row within the estimate view, you will be presented with detailed information about that task.

{{< figure src="/images/tasks/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/tasks/estimatedetails.png" alt="" position="center" style="border-radius: 8px;" >}}

After execution, the logs are updated.

{{< figure src="/images/tasks/logrecords.png" alt="" position="center" style="border-radius: 8px;" >}}