+++
author = "Thomas Evensen"
title = "Version 3.0.0"
date = "2026-05-14"
tags = ["changelog","version 3.0.0"]
categories = ["changelog"]
+++

## Version 3.0.0 - May 14, 2026

Bugfix: Resolved the issue with adding tasks. Additionally, removed an annoying message regarding the missing configuration file.

The bug was caused by incorrect use of Swift concurrency in the Add function. The add and update tasks are asynchronous functions running on the @MainActor. The update was triggered by an unstructured task that completed after the caller was completed and cleared the values, causing the error.

To fix this, use structured concurrency with await. Await suspends execution until the async function completes.

Mastering Swift concurrency is challenging, and I’m learning daily. Swift concurrency and actor isolation in RsyncUI are minimized, but some model updates remain. I’m developing another app where Swift concurrency and actor isolation are essential, demonstrating mastery and highlighting areas for further learning.
