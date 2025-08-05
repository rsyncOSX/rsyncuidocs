+++
author = "Thomas Evensen"
title = "Version 2.6.3"
date = "2025-08-02"
tags = ["changelog","version 2.6.3"]
categories = ["changelog"]
+++

### Version 2.6.3 (build 157) - August 4, 2025

Here are the code updates for the upcoming release, scheduled to be released before the end of August 2025:

#### Dev build #1 - August 4

- the RsyncUI application icon has been updated using the new Apple Icon Composer
 	- this update supports icons in the new macOS Tahoe 26 and incorporates layered icons, the icon has also undergone a slight redesign, featuring a new cloud and numbers as layers in Icon Composer
- the progress bar displayed during file synchronization has been set to have a fixed width, limiting the maximum number of transferred files
- the Home catalogs view in the Tasks application has undergone a refactor
	- select the Home catalogs on the Toolbar in Tasks 
- A third method for observers, based on AsyncSequence, has been applied, please refer to blog post *Observers* for more details 
 	- this method is recommended for observing notifications, a crucial component of RsyncUI
 	- the third method was inspired by a blog post by Majid Jabrayilov, a frequent blogger about Swift and SwiftUI

The updated icon:

{{< figure src="/images/263/icon.png" alt="" position="center" style="border-radius: 8px;" >}}

The total number, like `9 068` below, is fixed on line:

{{< figure src="/images/263/progress.png" alt="" position="center" style="border-radius: 8px;" >}}

Assist in adding new catalogs, refactored to use pickers:

{{< figure src="/images/263/home.png" alt="" position="center" style="border-radius: 8px;" >}}


