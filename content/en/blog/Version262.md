+++
author = "Thomas Evensen"
title = "Version 2.6.2"
date = "2025-07-21"
tags = ["changelog","version 2.6.2"]
categories = ["changelog"]
+++

### Version 2.6.2 (build 156) - July 21, 2025 

Version 2.6.2 of RsyncUI require Xcode 26 and Swift 6.2 to compile. 

##### Updates in this release

There was a request to display the % of completed transfer pr file. It seems difficult to pick up the correct info if like `--info=progress2` is added as parameter to rsync. This parameter causes rsync to publish a lot of data, but it is difficult to get the correct info. You may test the parameter yourself by pasting the complete rsync command into a terminal window.  But, instead a counter completed files was easy to add. 

- only UI updates, no model changes
- added counter files completed and total number of files
    - the total number of files requiere an estimation run ahead of synchronization
    - the counter is displayed as part of the progress bar
- consistent use of *source* and *destination*
