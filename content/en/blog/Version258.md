+++
author = "Thomas Evensen"
title = "Version 2.5.8"
date = "2025-06-05"
tags = ["changelog","version 2.5.8"]
categories = ["changelog"]
+++

### Version 2.5.8 (build 152) - June 5, 2025 

This is a maintenance release.

In this release, I have decided to incorporate an internal refactor, a merge of two objects. Consequently, the version number will be updated to 2.5.8 build 152. While the refactor is not extensive, it does involve modifying numerous files. The merged object now maintain estimates, its actual results, and provide the real synchronization tasks with the max values to the progress bar. The capture of progress itself is done by the Process object.

The release is signed and notarized by Apple.

#### Changes within this release

There are quite a few minor updates:

- refactor, internal, merge of two objects for monitoring progress of estimation and the real synchronization task
- there was an issue with progress view during synchronization of a task by using "double click"
    - the first double click executes an estimate run, a -dry-run
    - the next double click executes the real synchronization of data
    - the bug causes the progress view is a spinning circular image and not the real progress
- if only one task, either selected or in configuration, when pressing *Magic Wand* for estimating task  within main Synchronize view, default progress view is presented and not number of tasks estimate is completed
    - the default progress view is a spinning circular image
    - if more than one task, the progress view presents the number of tasks estimate is completed
- in Profile view, now correct updating the profile picker when adding or delete profiles
    - the correct profile is actually loaded, but profile picker is not correctly set
- removed profile name from most tables, display profile name in heading view
    - makes more room for display other info in tables
- internal refactor, every time a "/", forward slash, is added, using the library function `.appending(_other: some StringProtocol)`
    - before used the `+` sign, like `string + "/"`, after refactor  `string.appending("/")`
- fixed updating profile picker when RsyncUI discover new mounts and automatically loads profile
    - within the released version the profile picker does not show the correct profile loaded
    - the correct profile is actually loaded
- removed the weekly option from Calendar, only once and daily are schedule options
- within the Verify remote view, changed the toggle for delete parameter in pull and push
    - when choosing either pull or push, the delete parameter is included as default
 
The blog "Number of files" presents the number of files in RsyncUI. Within this release there are 228 Swift files and 17,880 lines of code.
