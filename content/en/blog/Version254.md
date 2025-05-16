+++
author = "Thomas Evensen"
title = "Version 2.5.4"
date = "2025-05-16"
tags = ["changelog","version 2.5.4"]
categories = ["changelog"]
+++

### Version 2.5.4 (build 146) - not yet released

This will be a maintenance release, and it is likely to be released by the end of May 2025. In the latest release, there were several UI updates and some minor updates that were not included in the latest release. For the next few weeks, I will conduct some quality assurance testing of the UI and update this blog with information about any minor issues that are found and updates.

- if any native English speaking users have some comments about the term "folder" and "directory", please notify me
    - see blog about released version 2.5.3
- in Tasks, view for adding new tasks, pressing the Enter key does not jump to the next logical field in view
    - fixed in code, pressing Enter key automatically jumps to next input field and by end automatically adds new task
    - workaround, manually select field to add value
- in QuickTasks, RsyncUI flips local and remote when executing a syncremote task, aka pull data from remote to local
    - Quicktask is also only valid if there is a remote server involved, for local attached volumes use the macOS Finder