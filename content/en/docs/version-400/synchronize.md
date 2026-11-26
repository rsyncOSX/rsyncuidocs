+++
author = "Thomas Evensen"
title = "Synchronize and estimate"
linkTitle = "1. Synchronize"
date = "2026-11-26"
weight = 10
description = "The new Synchronize workspace and the Estimate (Dry Run) result."
tags = ["version 4.0.0"]
categories = ["version 4.0.0"]
+++

## The Synchronize workspace

{{< figure src="/images/version400/nr1.png" alt="Synchronize workspace" position="center" style="border-radius: 8px;" >}}

The main window opens in **Synchronize**. The sidebar holds the profile picker, *Actions* (Synchronize, Tasks) and *Tools* (Restore, Profiles), with the rsync version at the bottom. The task table shows each task with its source, destination (server and path) and when it last ran. The run bar at the bottom has **Estimate (Dry Run)** and **Synchronize**, and the toolbar has **Estimate & Sync**, **Reset** and a filter by Synchronize ID.

## Estimate (Dry Run)

{{< figure src="/images/version400/nr2.png" alt="Estimate result" position="center" style="border-radius: 8px;" >}}

The result of an estimate. Summary cards at the top show files **Created**, **Transferred**, **Deleted** and the **Transfer size** for all tasks. The table shows the numbers per task; tasks with changes are highlighted in blue. Here only *GitHub backup* has changes. Click **Synchronize** to run the estimated tasks.
