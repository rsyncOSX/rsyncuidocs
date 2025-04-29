+++
author = "Thomas Evensen"
title = "Swift concurrency"
date = "2025-03-01"
tags = ["swift concurrency", "asynchronous"]
categories = ["technical details"]
+++

To commence, I must acknowledge that my comprehension of Swift concurrency is limited. RsyncUI is a graphical user interface (GUI) application; the majority of its operations are executed on the main thread. However, some resource-intensive tasks are performed on separate threads, excluding and not blocking the main thread. 

The most important work are executed on the main thread. By default, SwiftUI makes sure all UI-updates are performed on the main thread. Below are other tasks executed on the main thread:

- preparing of and execution of `rsync` synchronize tasks
- monitoring progress and termination of tasks
- write operations of logdata of synchronize tasks to storage

All read and write operations, transmission of the synchronized data is outside control of RsyncUI and taken care of by `rsync` itself.

#### Swift concurrency and asynchronous execution

Concurrency and asynchronous execution are important parts in Swift. The latest version of Swift simplifies the writing of asynchronous code using Swift `async` and `await` keywords, as well as the `actor` protocol. RsyncUI does not require concurrency, but concurrency is automatically introduced by using `actors` , `async` and `await` keywords. It is an objective to execute most work synchronous on the main thread as long as it does not block the GUI.

The Swift concurrency model is intricate, and it requires, at least for me, dedicated time and study to understand its fundamentals. 

#### Swift version 6 and the new concurrency model

Swift version 6 introduced strict concurrency checking. By enabling *Swift 6 language mode*  and *strict concurrency checking*, Xcode assists in identifying and resolving possible data races at compile time.

Quote swift.org: *"More formally, a data race occurs when one thread accesses memory while the same memory is being modified by another thread. The Swift 6 language mode eliminates these issues by preventing data races at compile time."*

RsyncUI adheres to the new concurrency model of Swift 6.

#### Other threads and RsyncUI

In Swift, concurrency is either unstructured or structured. While I am not an expert in this field, I will refrain from delving into the intricacies of the distinction between the two.  The following tasks are executed on a single isolated thread, adhering to the `actor` protocol:

- reading operations
- data decoding and encoding
- sorting log records
- preparing output from rsync for display
- preparing data from the logfile, not logrecords, for display
- checking for updates to RsyncUI

Adhering to the actor protocol, all access to properties within an actor must be performed asynchronously. 

The above mentioned tasks are executed on other threads than the`@MainActor`. The runtime environment handles scheduling and execution, guaranteeing that all functions within an actor are  `nonisolated func`, which, to my understanding, guarantees their execution on the global executor and prevents blocking of the main thread.

##### Structured concurrency

Some concurrent functions within RsyncUI are structured by using `async let`. You may have several `async let`, and they will all be executed in parallel or concurrent. When all `async let` tasks are completed, the calling function or parent, will evaluate the result and continue execution. 

```swift
func readconfigurations() {
    
    Task {
        ....
      	async let readconfigurations = ActorReadSynchronizeConfigurationJSON()
            rsyncUIdata.configurations = await readconfigurations
                .readjsonfilesynchronizeconfigurations(selectedprofile,
                                                       SharedReference.shared.monitornetworkconnection,
                                                       SharedReference.shared.sshport)
        ....
	}
}
```

##### Unstructured concurrency

The code snippet below presents an *unstructured* concurrency.  The code within the `Task  { ... }` *may* be completed after the execution of the calling function, the parent,  is completed.  Upon the function's return, the UI is notified on the main thread if there is a new version available.

```swift
@MainActor
func somefunction() {
    ....
    Task {
      newversion.notifynewversion = await GetversionofRsyncUI().getversionsofrsyncui()
	}
    ....
}
```

```swift
actor GetversionofRsyncUI {
    nonisolated func getversionsofrsyncui() async -> Bool {
        do {
            let versions = await DecodeGeneric()
            if let versionsofrsyncui =
                try await versions.decodearraydata(VersionsofRsyncUI.self,
                                                   fromwhere: Resources().getResource(resource: .urlJSON))
            {
                let runningversion = Bundle.main.infoDictionary?["CFBundleShortVersionString"] as? String ?? ""
                let check = versionsofrsyncui.filter { runningversion.isEmpty ? true : $0.version == runningversion }
                if check.count > 0 {
                    return true
                } else {
                    return false
                }
            }
        } catch {
            return false
        }
        return false
    }
}
```





