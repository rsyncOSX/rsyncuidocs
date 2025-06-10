+++
author = "Thomas Evensen"
title = "Version 2.5.9"
date = "2025-06-10"
tags = ["changelog","version 2.5.9"]
categories = ["changelog"]
+++

### Version 2.5.9 (build 153) - not yet released

This blog serves as a notification regarding the upcoming version of RsyncUI. In the previous released version I implemented a refactoring of the profile picker to enable the handling of nil values, following a tutorial I discovered. Upon further examination of the code, I conducted additional cleanup and eliminated unnecessary code. 

Another internal refactor is combining all objects for preparing, estimation and execution of tasks. *Prepare* is collect either all tasks, selected tasks or estimated tasks with data to synchronize. The combined object stores a stack of *prepared tasks*. During estimation and execution, the object pops the first task of the stack, computes arguments and initiates a Process object for execute of the command  `rsync`. When a process termination is observed, the next tasks is popped of the stack and the process is repeated until the stack is empty. 

By combining the above objects it is easier to read the code and eliminated unnecessary code.

The code within the most recent released version adheres to the expected behavior. However, whenever possible, I strive to achieve the same result with lesser code. Lesser code is better code.

 Cleanup of code is the major work in next version. And there *will* be some minor fixes well. To be released sometime in July 2025. 

The GitHub repository is updated. You may browse changes in code by view  [latest release](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.5.8). The main repository is committed with latest changes.