+++
author = "Thomas Evensen"
title =  "Synchronize data"
date = "2025-02-10"
tags = ["synchronize"]
categories = ["synchronize"]
+++

{{< alert >}}

The *Synchronize* view enables the execution of either all or selected tasks in a single operation, either by *shortcut actions* or by *functions* on the toolbar.

Or, for a single task, a double-click *on one task* initiates a --dry-run (an estimate run), and the subsequent double-click executes the actual run for that task.

{{< /alert >}}

Shortcut actions within the *Synchronize* view:

- *estimate* - shortcut `⌘E` estimates all or selected tasks
- *synchronize* - shortcut `⌘R` synchronizes all or selected tasks without estimation
  - no progress bar during synchronization; a progress bar requires estimation first
- *abort* - shortcut `⌘K` aborts and halts any ongoing task

Upon launching RsyncUI, it automatically opens the *Synchronize* view. Selecting the *wand and stars* (shortcut `⌘E`) from the toolbar initiates estimation of all tasks.

{{< figure src="/images/tasks/tasks.png" alt="" position="center" style="border-radius: 8px;" >}}

The outcome of an estimate is displayed, with blue numbers indicating data that requires synchronization. To execute the actual synchronization tasks directly from the summarized estimate view, press the left arrow (shortcut `⌘R`) on the toolbar.

By selecting a row within the estimate view, you will be presented with detailed information about that task.

{{< figure src="/images/tasks/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/tasks/estimatedetails.png" alt="" position="center" style="border-radius: 8px;" >}}

After execution, the logs are updated.

{{< figure src="/images/tasks/logrecords.png" alt="" position="center" style="border-radius: 8px;" >}}