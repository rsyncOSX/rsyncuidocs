+++
author = "Thomas Evensen"
title = "Version 2.6.0"
date = "2025-06-27"
tags = ["changelog","version 2.6.0"]
categories = ["changelog"]
+++

### Version 2.6.0 (build 154) - work in progress 

There is a new beta of Xcode and Swift 6, Xcode 26 and Swift 6.2. There are some new features regarding concurrency in Swift 6.2 and I have just started to read and learn more about them. There are three branches on the GitHub repository now. The Xcode 26 branch `version-2.6.0-xcode26` includes only some concurrency specific features. This branch require Xcode 26 to compile. All branches are apart from the concurrency specific parts, updated with latest development.

Xcode 16.4 and Swift 6.1

- `main` and `version-2-6-0`branch

Xcode 26 and Swift 6.2 beta

- `version-2.6.0-xcode26` branch

The GitHub Desktop now includes generating commit comments by GitHub Copilot. From version 2.6.0 of RsyncUI there is more info about the commits. 

### Macos 26 Tahoe

I have tested installing, by Homebrew, the latest version of RsyncUI on a virtual macOS 26 Tahoe. I did also install the latest version of rsync by Homebrew. And by a short test only, both RsyncUI and the latest version of rsync did run as expected. 

When Apple releases a *public beta* of macOS 26 Tahoe, I will install it and investigate if I will adapt some  macOS 26 Tahoe specific changes to RsyncUI. RsyncUI will still be **supported** for the last three versions of macOS.

