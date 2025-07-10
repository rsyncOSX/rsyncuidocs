+++
author = "Thomas Evensen"
title = "Version 2.6.0"
date = "2025-07-10"
tags = ["changelog","version 2.6.0"]
categories = ["changelog"]
+++

### Version 2.6.1 (build 155) - July 10, 2025 

Version 2.6.1 of RsyncUI require Xcode 26 and Swift 6.2 to compile. 

##### Updates in this release

- if Colorscheme is Light there are some issues with text colors, the last issue is resolved regarding text colors
    - the issue applies only if using Light Colorscheme
    - I was not aware of the issues, on both my Macs I was using Dark Colorscheme, now I am using Light Colorscheme on one of my Macs
- the Calendar is renamed to Schedule, and there was an issue loading schedules for "Default" profile
    - The Schedule is by default hidden, you may enable it in user settings
- after an estimate run, the Estimate column within main Synchronize view is removed, the Synchronize ID is tagged with color instead and during estimation prefixed by an arrow
- profile picker is hidden if only Default profile in use
    - if a new profile is added, the profile picker is present
    - also applies to profile picker if Sidebar menu is hidden
- in Tasks view, buttons for saving URL strings are refactored
    - the URL strings are added to Rsync Parameters view
- refactor of the Verify Remote function, caution this is a special function and please read about it within the Documentation,  refer to the *Verify remote* section.
    - the output, estimates, from both pull and push are now by default not adjusted
    - there are added three colors for rows tagged for: delete, pull and push, it might assist in deciding push or pull
    - from the result of push and pull, go direct to either push or pull view
- refactor of write and read to logfile as actor, writing and reading to logfile is now on a background thread
- the Import function is refactored
    - see File->Export & Import->Import
- added new concurrency keywords
    - new keywords included Swift version 6.2

And there is a detailed changelog from the release page GitHub. There are not any updates or refactors to the main parts of RsyncUI, like estimation, execution, process apart from some new concurrency keywords (Swift 6.2) added to the actors.

#### New concurrency keywords and AI generated commit comments

There is a new beta of Xcode and Swift 6, Xcode 26 and Swift 6.2. There are some new features regarding concurrency in Swift 6.2 and I have just started to read and learn more about them. The GitHub Desktop now includes generating commit comments by GitHub Copilot. From version 2.6.0 of RsyncUI there is more info about the commits. 

#### Macos 26 Tahoe

I have tested installing, by Homebrew, the latest version of RsyncUI on a virtual macOS 26 Tahoe. I did also install the latest version of rsync by Homebrew. And by a short test only, both RsyncUI and the latest version of rsync did run as expected. 

And I have commenced some testing and development on the virtual macOS 26 Tahoe and Xcode 26 beta. It might be some macOS 26 Tahoe specific changes to RsyncUI, but it will still **support**  for the last three versions of macOS. Any macOS 26 Tahoe specific changes are handled by compiler directives in code. 

