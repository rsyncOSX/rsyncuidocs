---
title: RsyncUI - a GUI for rsync
linkTitle: Documentation
menu: { main: { weight: 20 } }
---

*RsyncUI* is a macOS application developed using Swift and SwiftUI, designed for macOS Sonoma and subsequent versions. It leverages the command-line tool rsync for file synchronization. Notably, rsync executes the synchronization tasks, while RsyncUI provides a graphical user interface (GUI) on top of rsync. 

RsyncUI is a complimentary and open-source application. Kindly review the MIT license before commencing to use RsyncUI. RsyncUI is 100% open-source software and will always remain free.

<div class="alert alert-secondary" role="alert">

RsyncUI is *digitally signed* and *notarized* by Apple, ensuring its security and preventing malicious code and tampering. However, RsyncUI is not sandboxed, which is a requirement for macOS applications on the Apple App Store. The App Sandbox imposes certain restrictions on the functionality of an application within its environment. A sandboxed app cannot read hidden directories such as `.ssh` or `.rsyncosx` from the user's home directory. Additionally, it cannot use rsync installed by Homebrew. Sandboxing RsyncUI would render it ineffective.

</div>

### Concealing Actions

Additional information regarding Concealing Actions can be found in the *Getting started* section. To toggle the visibility of actions on the main toolbar in RsyncUI, press the shortcut `⌘S`.

### Privacy statement

RsyncUI is a desktop application only, there is no server component. It does not generate any logs that are transmitted from your Mac. Data pertaining to tasks and logs is stored locally on your Mac as files. You can backup all files created by RsyncUI to the Document directory on your Mac from the Settings view. The sole data transferred from your Mac to a server occurs only if you enable tasks with a remote server destination. You bear sole responsibility for securing your own data if synchronized to a remote server.

### Changelog and Installation

For the most up-to-date information, please refer to the [changelog](/blog/). RsyncUI is constructed as a Universal macOS Binary, ensuring native execution on Apple Silicon and Intel-based Mac computers.

RsyncUI can be installed via Homebrew or downloaded from [GitHub](https://github.com/rsyncOSX/RsyncUI/releases/).
```bash
brew install --cask rsyncui
```

If installed via Homebrew, the SHA-256 hash is automatically verified. For downloads from GitHub, please verify the SHA-256 hash manually.