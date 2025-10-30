+++
author = "Thomas Evensen"
title = "Version 2.7.6"
date = "2025-10-30"
tags = ["changelog","version 2.7.6"]
categories = ["changelog"]
+++

### Version 2.7.6 (build 167) - 30 October, 2025 release candidate

Please download and test the rc.

A few users have experienced a crash when estimating tasks. I was unable to determine the cause of the issue until today. Today, I successfully induced RsyncUI to crash with the same crash log as reported, which is a promising step towards resolving the issue.

{{< alert color="warning" >}}

It is of utmost importance that the updated code functions as intended. A release candidate for testing purposes has been released. In addition to resolving the identified issue, the updated code introduces an enhancement in both data estimation and synchronization. The increased speed observed in RsyncUI’s data reading from the rsync process is not directly related to the actual synchronization of data, which is managed independently of RsyncUI.

{{< /alert >}}

#### The updated code 

The code is a component of the Process object, which is a small object. However, RsyncUI is entirely dependent on the object functioning correctly. The object outputs data from the rsync process and detects the termination signal when the rsync process is completed. 

The issue appears to be that the termination and release of objects are sometimes executed before all output data is processed. If the object is released and the process attempts to handle output, it will result in a crash. The new code no includes a *drain* of output before the termination process is executed. And it also seems to gain a speed increase in estimating.

The updated part of code is now:

```
let sequencefilehandler = NotificationCenter.default.notifications(named: NSNotification.Name.NSFileHandleDataAvailable, object: nil)
let sequencetermination = NotificationCenter.default.notifications(named: Process.didTerminateNotification, object: nil)
    
// Tasks
var sequenceFileHandlerTask: Task<Void, Never>?
var sequenceTerminationTask: Task<Void, Never>?

...

sequenceFileHandlerTask = Task {
            for await _ in sequencefilehandler {
                if self.getrsyncversion == true {
                    await self.datahandlersyncversion(pipe)
                } else {
                    await self.datahandle(pipe)
                }
            }
            // Final drain - keep reading until no more data
            while pipe.fileHandleForReading.availableData.count > 0 {
                Logger.process.info("ProcessRsyncVer3x: sequenceFileHandlerTask - drain remaining data")
                if self.getrsyncversion == true {
                    await self.datahandlersyncversion(pipe)
                } else {
                    await self.datahandle(pipe)
                }
            }
        }

sequenceTerminationTask = Task {
            for await _ in sequencetermination {
                // Small delay to let final data arrive
                try? await Task.sleep(nanoseconds: 100_000_000) // 0.1 seconds
                await self.termination()
            }
        }        
```

