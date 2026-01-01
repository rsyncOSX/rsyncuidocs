+++
author = "Thomas Evensen"
title = "Tagging of data"
date = "2025-03-01"
tags = ["tagging"]
categories = ["technical details"]
+++

### Overview

{{% pageinfo color="info" %}}

RsyncUI must tag data accurately; otherwise some source data might not synchronize. RsyncUI supports both the latest rsync release and the legacy macOS default.

{{% /pageinfo %}}

Tagging is computed in the ParseRsyncOutput Swift package bundled with RsyncUI.

**Example:**

- Input string: `Number of created files: 7,191 (reg: 6,846, dir: 345)`
- Converted to: `[7191, 6846, 345]` (the thousands separator is also removed from the string before parsing)

The function below extracts only numbers from the input:
```swift
public func returnIntNumber(_ input: String) -> [Int] {
    var numbers: [Int] = []
    let str = input.replacingOccurrences(of: ",", with: "")
    let stringArray = str.components(separatedBy: CharacterSet.decimalDigits.inverted)
                         .compactMap { $0.isEmpty == true ? nil : $0 }
    for item in stringArray where item.isEmpty == false {
        if let number = Int(item) {
            numbers.append(number)
        }
    }
    if numbers.count == 0 {
        return [0]
    } else {
        return numbers
    }
}
```

Parsing the rsync output is straightforward, but the formats differ between the latest rsync release and the default macOS version.

### Version 3.4.x 

The trailing output from the latest version of rsync (version 3.4.1) looks like:
```
....
Number of files: 7,192 (reg: 6,846, dir: 346)
Number of created files: 7,191 (reg: 6,846, dir: 345)
Number of deleted files: 0
Number of regular files transferred: 6,846
Total file size: 24,788,299 bytes
Total transferred file size: 24,788,299 bytes
Literal data: 0 bytes
Matched data: 0 bytes
File list size: 0
File list generation time: 0.003 seconds
File list transfer time: 0.000 seconds
Total bytes sent: 394,304
Total bytes received: 22,226
sent 394,304 bytes  received 22,226 bytes  833,060.00 bytes/sec
total size is 24,788,299  speedup is 59.51 (DRY RUN)
```

### Openrsync 

The trailing output from the default version of rsync looks like:
```
....
Number of files: 7192
Number of files transferred: 6846
Total file size: 24788299 bytes
Total transferred file size: 24788299 bytes
Literal data: 0 bytes
Matched data: 0 bytes
File list size: 336861
File list generation time: 0.052 seconds
File list transfer time: 0.000 seconds
Total bytes sent: 380178
Total bytes received: 43172
sent 380178 bytes  received 43172 bytes  169340.00 bytes/sec
total size is 24788299  speedup is 58.55
```

### How the Tagging Works

The output from rsync is parsed and numbers are extracted. After parsing, these numbers determine whether data should be tagged for synchronization.

#### Latest Version of rsync

Three numbers decide whether data needs synchronization: updates (regular files transferred), new files, and deleted files. Each can be zero or positive, and all three are checked.

#### Default Versions

Only one number decides: the updates (files transferred).