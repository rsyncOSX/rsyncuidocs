+++
author = "Thomas Evensen"
title = "Version 2.9.4"
date = "2026-05-02"
tags = ["changelog","version 2.9.4"]
categories = ["changelog"]
+++

### Version 2.9.4 - May 02, 2026 (not released)

A cleanup of code in RsyncUI is underway. RsyncUI is stable and has many downloads, but I learned more about concurrency and caching while working on another project that requires it. RsyncUI lacks caching, and most work is done on the main thread. There’s a minor need for concurrency and isolation mechanisms like actors in the code. However, concurrency is used to avoid blocking the UI during reading, writing, and sorting log records. All other read and sorting are executed on the main actor. As well as the real synchronization tasks and updates during synchronization.

The cleanup will take time, and I’m unsure how aggressive I’ll be. I’m doing it in between projects. I don’t know when an updated version will be released, so don’t hold your breath. The most important thing is to keep the code updated.

There has also been an update in package RsyncAnalyse due to changes in the output by applying the `--itemize-changes` in newly released rsync version 3.4.2. Apart from that there are no changes in the output in version 3.4.2 of rsync and there is no need for other updates in RsyncUi due to this release of rsync.

## AI

I use AI to discover and plan updates. Follow the updates in the markdown docs like `phase1.md` and `phase4.md` in the `version 2.9.4-cleanup` branch. The next version will be a release candidate when ready. There will be several updates, with two or three releases before completion. I won't make a major new release until I'm certain no bugs are introduced.