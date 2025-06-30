+++
author = "Thomas Evensen"
title = "Version 2.6.0"
date = "2025-06-30"
tags = ["changelog","version 2.6.0"]
categories = ["changelog"]
+++

### Version 2.6.0 (build 154) - development build 

Version 2.6.0 of RsyncUI require Xcode 26 and Swift 6.2 to compile.

Build by *Xcode 26 beta 2, Swift 6.2* on *macOS 15.5 Sequoia* (not macOS 26 Tahoe). I will from time to time release new builds of version 2.6.0 until macOS 26 Tahoe is released. The build is based upon the `version-2.6.0-xcode26` branch.

There are not any updates or refactors to the main parts of RsyncUI, like estimation, execution, process and so on apart from some new concurrency keywords added to the actors. This means the development build is as stable as the released version. But changes might introduce some issues to the UI part only. 

Changes June, 30:

- profile picker is hidden if only Default profile in use
    - if a new profile is added, the profile picker is present
    - also applies to profile picker if Sidebar menu is hidden
- in Tasks view, buttons for saving URL strings are refactored
    - the URL strings are added to Rsync Parameters view
- text colors are now Colorscheme aware, black if light scheme and white if dark scheme

Changes June, 27:

- refactor of the Verify Remote function, caution this is a special function and please read about it within the Documentation,  refer to the *Verify remote* section.
    - the output, estimates, from both pull and push are now by default not adjusted
    - there are added three colors for rows tagged for: delete, pull and push, it might assist in deciding push or pull
    - from the result of push and pull, go direct to either push or pull view
- the Calendar function my by hidden from main Sidebar, on by default
    - set in RsyncUI Settings
- after an estimate run, the Estimate column within main Synchronize view is removed, the Synchronize ID is tagged with color instead
- refactor of write and read to logfile as actor, writing and reading to logfile is now on a background thread
- the Import function is refactored,  see File->Export & Import->Import
- added new concurrency keywords, new keywords included Swift version 6.2

And there is a detailed changelog from the release page GitHub.

#### Development in progress

There is a new beta of Xcode and Swift 6, Xcode 26 and Swift 6.2. There are some new features regarding concurrency in Swift 6.2 and I have just started to read and learn more about them. The GitHub Desktop now includes generating commit comments by GitHub Copilot. From version 2.6.0 of RsyncUI there is more info about the commits. 

#### Macos 26 Tahoe

I have tested installing, by Homebrew, the latest version of RsyncUI on a virtual macOS 26 Tahoe. I did also install the latest version of rsync by Homebrew. And by a short test only, both RsyncUI and the latest version of rsync did run as expected. 

And I have commenced some testing and development on the virtual macOS 26 Tahoe and Xcode 26 beta. It might be some macOS 26 Tahoe specific changes to RsyncUI, but it will still **support**  for the last three versions of macOS. Any macOS 26 Tahoe specific changes are handled by compiler directives in code. 

