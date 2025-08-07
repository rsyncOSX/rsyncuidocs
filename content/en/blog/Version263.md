+++
author = "Thomas Evensen"
title = "Version 2.6.3"
date = "2025-08-07"
tags = ["changelog","version 2.6.3"]
categories = ["changelog"]
+++

### Version 2.6.3 (build 157) - August 7, 2025

Here are the code updates for the upcoming release, scheduled to be released before the end of August 2025:

#### Dev build #2 - August 7

- within Tasks, the option for trailing slash is refactored:
	- *Add* trailing slash, add a trailing slash to source and destination
	- *Do not add* trailing slash, don’t add or if added remove
	- *Do not check*, accept whatever is added, slash or no slash on either
- within Tasks, the values for *Action* and *Trailing /* is saved during the session if set to other than default values 
	- values “survive" Add, Update and change profile
    - values are temporary saved in UserDefaults
    - when RsyncUI restarts, the above values is set to default values

Either source or destination is allowed to be empty.

{{< figure src="/images/263/slash.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Dev build #1 - August 4

- the RsyncUI application icon has been updated using the new Icon Composer tool
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
