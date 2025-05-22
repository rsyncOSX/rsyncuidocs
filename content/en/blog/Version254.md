+++
author = "Thomas Evensen"
title = "Version 2.5.4"
date = "2025-05-19"
tags = ["changelog","version 2.5.4"]
categories = ["changelog"]
+++

### Version 2.5.4 (build 146) - May 19, 2025 release candidate

This will be a maintenance release, and it is likely to be released by the end of May 2025. In the latest release, there were several UI updates and some minor updates that were not included in the latest release. For the next few weeks, I will conduct some quality assurance testing of the UI and update this blog with information about any minor issues that are found and updates.

- if any native English speaking users have some comments about the term "folder" and "directory", please notify me
    - see blog about released version 2.5.3
- in Tasks, view for adding new tasks, pressing the Enter key does not jump to the next logical field in view
    - *fixed in release candidate*
    - pressing Enter key automatically jumps to next input field and by end automatically adds new task
    - workaround, manually select field to add value
- in QuickTasks, RsyncUI flips local and remote when executing a syncremote task, aka pull data from remote to local
    - *fixed in release candidate*
    - Quicktask is also only valid if there is a remote server involved, for local attached volumes use the macOS Finder
- there is a minor issue selecting a task for adding parameters to rsync within the Rsync parameters view
    - *fixed in release candidate*
    - the issue occurs if there is selected a task in the main Synchronize view, switch to Rsync parameters view, selecting the task will not enable adding parameters to rsync
    - workaround, deselect task in main Synchronize view and return to Rsync parameters view
    - the issue is caused due to the fix for situation where RsyncUI become unresponsive with a bouncing beach ball, see comments for blog about version 2.5.3

#### Version 2.5.5 (build 147) - to be released as maintenance release

To be released by end of May 2025. It is a new version number to include notification to users of the release candidate about a new vesion as well. There are also some new internal refactory of code.

- I did read a blog about Picker and nil values and how to deal with optional values
    - a Picker is like the profile selector and optional values may be `nil`
    - when a new user commence using RsyncUI, there are no profiles but only the default path
    - a profile is only a catalog and RsyncUI stores data for that profile in that catalog
- if you have ON *"Observe mounting of external drives"* in settings, RsyncUI will automatically load profile if mounted volume path in destination
    - when unmounting the volume, RsyncUI now also automatically load default profile
    - the automated selection of profile is only valid if there is created one or more profile