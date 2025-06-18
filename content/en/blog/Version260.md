+++
author = "Thomas Evensen"
title = "Version 2.6.0"
date = "2025-06-18"
tags = ["changelog","version 2.6.0"]
categories = ["changelog"]
+++

### Version 2.6.0 (build 154) - work in progress 

I have commenced development of next version by using Xcode 26 beta which includes Swift version 6.2. This version of code is checked in at GitHub as branch `version-2.6.0-xcode26`. This branch will NOT compile using latest released Xcode version 16.4. There are a few new compiler directives for concurrency in Xcode 26 and there are some changes to the concurrency as well in Swift 6.2. 

I have applied changes to all actors in this branch, as well as converted and refactored the object for writing to logfile to an actor. There will also be some new minor enhancements to this version when released. 

When Apple releases a *public beta* of macOS 26 Tahoe, I will install it and investigate if I should do adapt some Tahoe specific changes to RsyncUI. RsyncUI will still be supported for the last three versions of macOS. 

