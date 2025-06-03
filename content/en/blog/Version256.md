+++
author = "Thomas Evensen"
title = "Version 2.5.6"
date = "2025-06-03"
tags = ["changelog","version 2.5.6"]
categories = ["changelog"]
+++

### Version 2.5.6 (build 150) - June 3, 2025 a development release

The development builds maintain the same version number while updating the build number. The changelog will meticulously document changes and the corresponding build numbers. Eventually, the development will be released as a new version later this summer. 

All development builds are signed and notarized by Apple.

#### Build 150, June 3:

This is most likely the last development build before a new maintenance release. If no issues are reported this will be released as version 2.5.7 build 151 by a end of this week.

- there was an issue with progress view during synchronization of a task by using "double click"
    - the first double click executes an estimate run, a -dry-run
    - the next double click executes the real synchronization of data
    - the bug causes the progress view is a spinning circular image and not the real progress

The bug was caused by a mistake in not assigning data within a concurrent code. The root function, the calling function of the concurrent code, was completed before the concurrent code was completed. The assignment of data is now part of the concurrent code, and the assignment is executed when the asynchronous function is completed. Concurrency in code really require to be aware what is happening and to understand the basics.

#### Build 149, May 31:

- if only one task, either selected or in configuration, when pressing *Magic Wand* for estimating task  within main Synchronize view, default progress view is presented and not number of tasks estimate is completed
    - the default progress view is a spinning circular image
    - if more than one task, the progress view presents the number of tasks estimate is completed
- in Profile view, now correct updating the profile picker when adding or delete profiles
    - the correct profile is actually loaded, but profile picker is not correctly set
- removed profile name from most tables, display profile name in heading view
    - makes more room for display other info in tables
- internal refactor, every time a "/", forward slash, is added, using the library function `.appending(_other: some StringProtocol)`
    - before used the `+` sign, like `string + "/"`, after refactor  `string.appending("/")`

#### Build 148, May 26:

- fixed updating profile picker when RsyncUI discover new mounts and automatically loads profile
    - within the released version the profile picker does not show the correct profile loaded
    - the correct profile is actually loaded
- removed the weekly option from Calendar, only once and daily are schedule options
- within the Verify remote view, changed the toggle for delete parameter in pull and push
    - when choosing either pull or push, the delete parameter is included as default
