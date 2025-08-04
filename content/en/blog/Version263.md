+++
author = "Thomas Evensen"
title = "Version 2.6.3"
date = "2025-08-02"
tags = ["changelog","version 2.6.3"]
categories = ["changelog"]
+++

### Version 2.6.3 (build 157) - not yet release

Here are the code updates for the upcoming release, scheduled to be released before the end of August 2025:

- the RsyncUI application icon has been updated using the new Apple Icon Composer.
 	- this update supports icons in the new macOS Tahoe 26 and incorporates layered icons, the icon has also undergone a slight redesign, featuring a new cloud and numbers as layers in Icon Composer.
- the progress bar displayed during file synchronization has been set to have a fixed width, limiting the maximum number of transferred files.
- the Home catalogs view in the Tasks application has undergone a refactor.
- A third method for observers has been introduced, please refer to blog post *Observers* for more details 
 	- this method is recommended for observing notifications, as it is a crucial component of RsyncUI, if one method is deprecated, it is secure to have two other methods if a refactor is required
 	- the third method was inspired by a blog post by Majid Jabrayilov, a frequent blogger about Swift and SwiftUI
 	- preliminary tests on macOS Tahoe 26 beta and macOS Sequoia will be conducted before the release of version 2.6.3 to assess the performance of the third method


New updated icon:

{{< figure src="/images/263/icon.png" alt="" position="center" style="border-radius: 8px;" >}}

The total number, like `9 068` below, is fixed on line:

{{< figure src="/images/263/progress.png" alt="" position="center" style="border-radius: 8px;" >}}

Assist in adding new catalogs, refactored to use pickers:

{{< figure src="/images/263/home.png" alt="" position="center" style="border-radius: 8px;" >}}


