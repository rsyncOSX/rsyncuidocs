---
title: RsyncUI - a GUI for rsync
linkTitle: Documentation
menu: { main: { weight: 20 } }
---

*RsyncUI* is a macOS application developed using Swift and SwiftUI, designed for macOS Sonoma and subsequent versions. It leverages the command-line tool rsync for file synchronization. Notably, rsync executes the synchronization tasks, while RsyncUI provides a graphical user interface (GUI) on top of rsync. RsyncUI is 100% open-source software and will remain absolutely free for all time.

RsyncUI is *digitally signed* and *notarized* by Apple, ensuring its security and preventing malicious code and tampering.

{{< alert color="warning" >}}

As a safety precaution, the --delete parameter is *not* set as a default parameter when adding new tasks. To ensure that the source and destination are in complete synchronization, the --delete parameter must be *enabled*. If you are new to `rsync`, I strongly recommend reading the *"Important"*  and *"Limitations"* sections as a minimum. 

{{< /alert >}}

{{< alert >}}

ChatGPT says the following: *In rsync documentation and usage, the most common terms are **source** and **destination**. These clearly indicate where the data is coming from and where it is going. While local and remote can be used when specifying locations across different systems, source and destination are universally applicable for both local and remote transfers.* In version, version 2.6.2, the terms have been revised to consecvent **source** and **destination**. The term **remote** is now exclusively used to refer to **remote user** and **remote server**. The user documentation to be updated as well.

{{< /alert >}}

{{< alert >}}

A note about the Schedule function: the schedule is implemented by using the Timer library. If your Mac goes to sleep, the schedule will NOT fire. If you lock your Mac, the schedule will NOT fire.  The schedule will only fire as long as your Mac is "awake" and you are *logged* in. Refer to the *Limitations* section. 

The Schedule is by default a hidden feature, enable in user settings.

{{< /alert >}}

### Privacy statement

RsyncUI is a desktop application only, there is no server component. It does not generate any logs that are transmitted from your Mac. Data pertaining to tasks and logs is stored locally on your Mac as files. You can backup all files created by RsyncUI to the Document directory on your Mac from the Settings view. The sole data transferred from your Mac to a server occurs only if you enable tasks with a remote server destination. You bear sole responsibility for securing your own data if synchronized to a remote server.

### Changelog and Installation

For the most up-to-date information, please refer to the [changelog](/blog/). RsyncUI is constructed as a Universal macOS Binary, ensuring native execution on Apple Silicon and Intel-based Mac computers.

RsyncUI can be installed via Homebrew or download from GitHub (https://github.com/rsyncOSX/RsyncUI/releases).

```bash
brew install --cask rsyncui
```

If installed via Homebrew, the SHA-256 hash is automatically verified. For downloads from GitHub, please verify the SHA-256 hash manually.
