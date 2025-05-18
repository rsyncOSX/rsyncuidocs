+++
author = "Thomas Evensen"
title = "Version 2.5.4"
date = "2025-05-18"
tags = ["changelog","version 2.5.4"]
categories = ["changelog"]
+++

### Version 2.5.4 (build 146) - not yet released

This will be a maintenance release, and it is likely to be released by the end of May 2025. In the latest release, there were several UI updates and some minor updates that were not included in the latest release. For the next few weeks, I will conduct some quality assurance testing of the UI and update this blog with information about any minor issues that are found and updates.

- if any native English speaking users have some comments about the term "folder" and "directory", please notify me
    - see blog about released version 2.5.3
- in Tasks, view for adding new tasks, pressing the Enter key does not jump to the next logical field in view
    - *fixed* in code
    - pressing Enter key automatically jumps to next input field and by end automatically adds new task
    - workaround, manually select field to add value
- in QuickTasks, RsyncUI flips local and remote when executing a syncremote task, aka pull data from remote to local
    - *fixed in code*
    - Quicktask is also only valid if there is a remote server involved, for local attached volumes use the macOS Finder
- there is a minor issue selecting a task for adding parameters to rsync within the Rsync parameters view
    - *fixed in code*
    - the issue occurs if there is selected a task in the main Synchronize view, switch to Rsync parameters view, selecting the task will not enable adding parameters to rsync
    - workaround, deselect task in main Synchronize view and return to Rsync parameters view
    - the issue is caused due to the fix for situation where RsyncUI become unresponsive with a bouncing beach ball, see comments for blog about version 2.5.3