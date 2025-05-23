+++
author = "Thomas Evensen"
title = "Version 2.5.5"
date = "2025-05-23"
tags = ["changelog","version 2.5.5"]
categories = ["changelog"]
+++

### Version 2.5.5 (build 147) - May 23, 2025

This is  a maintenance release. In the latest release, there were several UI updates. This release fixes some of the minor issues discovered after previous release. There is also one refactor of internal code, see comment about Picker and optional values.

- a few days ago I did read a blog about Picker and nil values and how to deal with optional values
    - a Picker is like the profile selector and optional values means there may be no selected value (`nil`)
    - when a new user commence using RsyncUI, there are no profiles but only the default path, the profile picker has no values but `nil` 
    - a profile is a folder and RsyncUI stores data for profile in folder (or directory), the profile name, displayed in profile picker,  is  name of the folder
- if you have ON *"Observe mounting of external drives"* in settings, RsyncUI will automatically load profile if mounted volume path in destination
    - when unmounting the volume, RsyncUI now also automatically load default profile
    - the automated selection of profile when mounting a volume is only valid if there is created one or more profiles
- in Tasks, view for adding new tasks, pressing the Enter key does not jump to the next logical field in view
    - pressing Enter key automatically jumps to next input field and by end automatically adds new task
- in QuickTasks, RsyncUI flips local and remote when executing a syncremote task, aka pull data from remote to local
    - Quicktask is also only valid if there is a remote server involved, for local attached volumes use the macOS Finder
- there is a minor issue selecting a task for adding parameters to rsync within the Rsync parameters view
    - the issue occurs if there is selected a task in the main Synchronize view, switch to Rsync parameters view, selecting the task will not enable adding parameters to rsync
    - the issue is caused due to the fix for situation where RsyncUI become unresponsive with a bouncing beach ball, see comments for blog about version 2.5.3
- the global replace function, in Tasks view, select the Globus on the toolbar
    - left text field part of text to be replaced
    - right text field replaced with what
    - any part of word may be replaced, as soon as you start type in the *replace field* the view is dynamically updated
