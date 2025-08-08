+++
author = "Thomas Evensen"
title = "Version 2.6.3"
date = "2025-08-07"
tags = ["changelog","version 2.6.3"]
categories = ["changelog"]
+++

### Version 2.6.3 (build 157) - August 7, 2025

Updates for the Upcoming Release (Scheduled for Release Before the End of August 2025):

#### Dev build #3 - not yet released

In both Home Catalogs and Quick task, the views have been refactored to utilize Form. Form offers a more streamlined and user-friendly interface. Additionally, data is now saved by default in UserSettings on macOS. When views are reentered, the data is automatically restored.

#### Dev build #2 - August 7

Within the Tasks section, the trailing slash option is refactored as follows:

* **Add trailing slash:** Add a trailing slash to both the source and destination.
* **Do not add trailing slash:** Do not add a trailing slash, or if added, remove it.
* **Do not check:** Accept the trailing slash regardless of whether it is present on either the source or destination.

Additionally, the values for the *Action* and *Trailing /* options are saved during the session if set to values other than the default. These values persist across Add, Update, and Profile changes. They are temporarily saved in UserDefaults and are reset to default values when RsyncUI restarts.

Either source or destination is allowed to be empty.


#### Dev build #1 - August 4

- The RsyncUI application icon has been updated using the new Icon Composer tool.
- This update supports icons in the new macOS Tahoe 26 and incorporates layered icons. The icon has also undergone a slight redesign, featuring a new cloud and numbers as layers in Icon Composer.
- The progress bar displayed during file synchronization has been set to have a fixed width, limiting the maximum number of transferred files.
- The Home catalogs view in the Tasks application has undergone a refactor.
	- Select the Home catalogs on the Toolbar in Tasks.
- A third method for observers, based on AsyncSequence, has been applied. Please refer to the blog post *Observers* for more details.
	- This method is recommended for observing notifications, a crucial component of RsyncUI.
	- The third method was inspired by a blog post by Majid Jabrayilov, a frequent blogger about Swift and SwiftUI.


#### Updated views

{{< figure src="/images/263/icon.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/263/progress.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/263/slash.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/263/home.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/263/quick.png" alt="" position="center" style="border-radius: 8px;" >}}
