+++
author = "Thomas Evensen"
title = "Swift concurrency"
date = "2025-03-01"
tags = ["swift concurrency", "asynchronous"]
categories = ["technical details"]
+++

> I’m developing a new macOS application, RawCull, that uses Swift concurrency in a unique way. My understanding of Swift concurrency is still limited, so I recommend exploring articles from experts in the field. However, RawCull also has a [technical blog](https://rawcull.netlify.app/blog/technical/) that covers how Swift concurrency is used to solve “heavy work” without blocking the UI. 

RsyncUI is a GUI app; most work happens on the main thread. Heavier tasks run on threads from the cooperative thread pool (CTP) without blocking the UI. The Swift runtime manages the executors and CTP. There are three kinds of executors:

- the *main executor* manages jobs on the main thread
- the *global concurrent executor* and the *serial executor* execute jobs on threads from the CTP

Most work in RsyncUI runs on the main thread. SwiftUI keeps UI updates there by default. Examples include:

- preparing and executing `rsync` synchronization tasks (including building arguments)
- monitoring progress and termination of `rsync` tasks
    - the collection of output from rsync is performed by an actor, while the actual reporting of the number of files transferred is executed on a main thread for UI updates
- some write and read operations

### Swift Version 6 and the New Concurrency Model

Swift version 6 introduced strict concurrency checking. By enabling *Swift 6 language mode* and *strict concurrency checking*, Xcode helps identify and resolve possible data races at compile time.

<div class="alert alert-danger" role="alert">

Several compiler directives in Xcode influence concurrency. Review them before migrating an existing project. I recommend the Swift concurrency posts by [Matt Massicotte](https://www.massicotte.org) and [Antoine van der Lee](https://www.avanderlee.com).

</div>

Quote from swift.org: *"More formally, a data race occurs when one thread accesses memory while the same memory is being modified by another thread. The Swift 6 language mode eliminates these issues by preventing data races at compile time."*

RsyncUI adheres to the Swift 6 concurrency model.

### Swift Concurrency and Asynchronous Execution

Swift makes asynchronous code more approachable through `async`, `await`, and `actor`. RsyncUI adopts these features even though most work can remain on the main thread—as long as it does not block the UI. Asynchronous work can happen on the main thread or on background threads from the CTP. On the main thread, structured concurrency with `async`/`await` is key; every `await` yields control so other tasks can proceed.

Some functions use `async let` for structured concurrency. Multiple `async let` bindings run concurrently, and execution resumes once they all complete. Structured concurrency also shapes ordering. Each `await` suspends until that async work finishes; sequential awaits run one after another.
