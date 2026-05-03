+++
author = "Thomas Evensen"
title = "Version 2.9.5rc"
date = "2026-05-03"
tags = ["changelog","version 2.9.5rc"]
categories = ["changelog"]
+++

## Version 2.9.5 - May 03, 2026 - test release

### Improved log and chart handling
 - Unified log-store loading behind a shared `LogStoreService`, so logging, log records, snapshots, and chart views now read from the same  source.
 - Centralized task/log lookup helpers for `hiddenIDs`, selected task resolution, and backup IDs, reducing repeated logic across the app.
 - Reworked log statistics chart preparation into a shared chart service/reducer pipeline.
 - Removed the older `ObservableChartData` path and added dedicated chart reducer tests.
 
### Improved persistence and async behavior
 - Replaced detached JSON writes with a shared awaited writer (`SharedJSONStorageWriter`) for configuration and log data.
 - Propagated the new async write flow through configuration updates, logging, imports, task creation/copy flows, and log deletion paths.
 - Removed thin actor wrappers for output formatting and version fetching, replacing them with simpler async helpers.
 
### Cleanup and simplification
 - Reduced app-owned actor usage down to the core log-related boundaries that still need serialization.
 - Removed older chart-related actor plumbing and several no-longer-needed adapter layers.
 - Removed the old “20 lines” tagging warning logic from estimate, execute, and task details code paths.
 
### Internal refactor progress
 - **Done:** shared log loading, shared configuration helpers, chart pipeline cleanup, detached JSON write removal, thin actor removal.
 - **Partial:** selection-to-log resolution is only partly centralized, and some async task bridges still remain.
 - **Not finished yet:** log delete-and-persist is still handled directly in some views, log-result parsing still exists in more than one  place, and snapshot/log merge logic is not fully unified yet.
 
### Notes
 - This changelog reflects the cleanup work merged in **PR #90** plus the follow-up commit that removed obsolete warning code.
 
### General comments

A cleanup of code in RsyncUI is underway. RsyncUI is stable and has many downloads, but I learned more about concurrency and caching while working on another project that requires it. RsyncUI lacks caching, and most work is done on the main thread. There’s a minor need for concurrency and isolation mechanisms like actors in the code. However, concurrency is used to avoid blocking the UI during reading, writing, and sorting log records. All other read and sorting are executed on the main actor. As well as the real synchronization tasks and updates during synchronization.

The cleanup will take time, and I’m unsure how aggressive I’ll be. I’m doing it in between projects. I don’t know when an updated version will be released, so don’t hold your breath. The most important thing is to keep the code updated.

There has also been an update in package RsyncAnalyse due to changes in the output by applying the `--itemize-changes` in newly released rsync version 3.4.2. Apart from that there are no changes in the output in version 3.4.2 of rsync and there is no need for other updates in RsyncUi due to this release of rsync.

### AI

I use AI to discover and plan updates. Follow the updates in the markdown docs like `phase1.md` and `phase4.md` in the `version 2.9.4-cleanup` branch. The next version will be a release candidate when ready. There will be several updates, with two or three releases before completion. I won't make a major new release until I'm certain no bugs are introduced.
