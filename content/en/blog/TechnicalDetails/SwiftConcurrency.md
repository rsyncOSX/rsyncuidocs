+++
author = "Thomas Evensen"
title = "Swift concurrency"
date = "2025-03-01"
tags = ["swift concurrency", "asynchronous"]
categories = ["technical details"]
+++

{{< alert >}}

To begin, I must admit that my knowledge of Swift concurrency is limited. I have a basic understanding of the subject, and if you are reading this blog and seeking further details about the topic, I recommend conducting a search and reading articles from other sources that provide a more comprehensive understanding of Swift concurrency.

{{< /alert >}}

RsyncUI is a graphical user interface (GUI) application; the majority of its operations are executed on the main thread. However, some resource-intensive tasks are performed on other threads managed the cooperative thread pool (CTP), excluding and not blocking the main thread. How to the executors and CTP works and interacts is details I dont know about, and it is managed by the Swift runtime. There are three kinds of executors:

- the Main Executor manage jobs on the Main Thread
- the global concurrent executor and the serial executor, both executes jobs on threads from the CTP

The most important work are executed on the Main Thread. By default, SwiftUI makes sure all UI-updates are performed on the Main Thread. Below are other tasks on the Main Thread:

- preparing of and execution of `rsync` synchronize tasks, preparing is computing the correct arguments for rsync 
- monitoring progress and termination of the real rsync tasks
- write operations of logdata of synchronize tasks to storage

All read and write operations, transmission of the synchronized data is outside control of RsyncUI and taken care of by `rsync` itself.

#### Swift concurrency and asynchronous execution

Concurrency and asynchronous execution are important parts in Swift. The latest version of Swift simplifies the writing of asynchronous code using Swift `async` and `await` keywords, as well as the `actor` protocol. RsyncUI does not require concurrency, but concurrency is automatically introduced by using `actors` , `async` and `await` keywords. It is an objective to execute most work synchronous on the main thread as long as it does not block the GUI.

#### Swift version 6 and the new concurrency model

Swift version 6 introduced strict concurrency checking. By enabling *Swift 6 language mode*  and *strict concurrency checking*, Xcode assists in identifying and resolving possible data races at compile time.

Quote swift.org: *"More formally, a data race occurs when one thread accesses memory while the same memory is being modified by another thread. The Swift 6 language mode eliminates these issues by preventing data races at compile time."*

RsyncUI adheres to the new concurrency model of Swift 6.

#### Cooperative thread pool (CTP)

The following tasks are executed asynchronous on threads from the CTP, adhering to the `actor` protocol:

- reading operations
- data decoding and encoding
- sorting log records
- preparing output from rsync for display
- preparing data from the logfile, not logrecords, for display
- checking for updates to RsyncUI

Adhering to the actor protocol, all access to properties within an actor must be performed asynchronously. There are three types of executors, which manages jobs and put jobs on threads for execution. 

The above mentioned tasks are executed on threads from the CTP, and not on the`@MainActor`. The runtime environment handles scheduling and execution, guaranteeing that all functions within an actor are  `nonisolated func`, which to my understanding, guarantees asynchronous execution on threads from the CTP.

##### Structured concurrency

Some concurrent functions within RsyncUI are structured by using `async let`. You may have several `async let`, and they will all be executed in parallel or concurrent. When all `async let` tasks are completed, the root task or parent task, will continue execution. 

```swift
func readconfigurations() async {
        ....
      	async let readconfigurations = ActorReadSynchronizeConfigurationJSON()
     	rsyncUIdata.configurations = await readconfigurations
         	.readjsonfilesynchronizeconfigurations(selectedprofile,
                                                   SharedReference.shared.monitornetworkconnection,
                                                   SharedReference.shared.sshport)
    
    	// after the await is completed, the root task will continue
    	// the structured concurrency is actually not needed here, only one async let
		....
	}
}
```

The below code is unstructured concurrency, the behaviour is as far as I understand equal for both.

```swift
func readconfigurations() async {
        ....
     	rsyncUIdata.configurations = await ActorReadSynchronizeConfigurationJSON()
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





