+++
author = "Thomas Evensen"
title = "After a shortcut run"
linkTitle = "5. The result"
date = "2026-11-26"
weight = 50
description = "Check the result of a shortcut run in RsyncUI."
tags = ["version 4.0.0"]
categories = ["version 4.0.0"]
+++

## Estimate after the run

{{< figure src="/images/version400/nr15.png" alt="Estimate after the shortcut run" position="center" style="border-radius: 8px;" >}}

The shortcut now runs without the message. RsyncUI estimates the tasks, synchronizes the ones with changes and quits by itself when done. A new estimate in RsyncUI afterwards shows zero changes for all tasks: the shortcut has synchronized *GitHub backup*.

## The log record

{{< figure src="/images/version400/nr16.png" alt="Log record written by the shortcut" position="center" style="border-radius: 8px;" >}}

The **Logs** tab for *GitHub backup* has a new record at the top (*410 files : 11.3 MB*), written by the shortcut run just like a run inside RsyncUI.
