+++
author = "Thomas Evensen"
title = "Version 2.5.9"
date = "2025-06-16"
tags = ["changelog","version 2.5.9"]
categories = ["changelog"]
+++

### Version 2.5.9 (build 153) - June 16, 2025 

This is as previous release, mostly a maintenance release. I have also, for test, compiled RsyncUI with the Xcode 26 beta. And it compiled with no errors as expected. There will be a new release when macOS Tahoa 26 and Xcode 26 with Swift version 6.2 is avaliable as release candidates. I dont know when this happens, but most likely in Sept or October sometime. And of course, if bugs are found a fix will be relased.

The following are changes in this release:

- a few internal refactors
    - three objects for estimation and execution are merged into one object, cleaner code and easier to read
    - two objects for montoring state within estimate and execute are removed, the Process object which executes the external rsync task is reporting when a the external task is sending a ProcessTermination signal
        - by this we know when a process starts, when it is in progress and when it is completed, dont need any state object for monitoring progress
    - removed not used properties like the profile name
        - the profile picker uses the UUID (the id) to compute the profile name when a new profile is selected
        - makes the code easier to read, less prone for errors when code is updated and less properties for RsyncUI to monitor
- added a couple of more checks before executing tasks
    - one check is if more than one task is selected, the double click function is disabled
- a few UI updates as well

Less code is better code. 

