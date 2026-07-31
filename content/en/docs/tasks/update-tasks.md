+++
author = "Thomas Evensen"
title =  "Update tasks"
date = "2025-02-09"
tags = ["update","profile"]
categories = ["synchronize"]
+++

To update a task, select it and press the update button to write changes to storage.

{{< figure src="/images/add/update.png" alt="" position="center" style="border-radius: 8px;" >}}

### Editing a task

Select the task in the task list. The Inspector opens on the right with tabs for **Edit**, **Parameters**, **Log Records**, and **Verify Task**. Make your changes in the relevant tab, then press the update button to save.

<div class="alert alert-danger" role="alert">

After changing any task parameter, always verify the task with a `--dry-run` before executing it. Select *"Verify tasks"* from the primary Sidebar menu.

</div>

### Halting and releasing tasks

Right-click a task and select **Halt** to temporarily disable it. A halted task shows a red stop sign in the action column and is excluded from estimates and execution. Right-click again and select **Release** to restore it; the task resumes with its original type.
