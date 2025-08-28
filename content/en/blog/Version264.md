+++
author = "Thomas Evensen"
title = "Version 2.6.4"
date = "2025-08-18"
tags = ["changelog","version 2.6.4"]
categories = ["changelog"]
+++

### Version 2.6.4 (build 158) - August 18, 2025

There are four major updates within this release:

- method for observers, based on *AsyncSequence*, has been applied, please refer to the blog post *Observers* for more details
- in Tasks, options for trailing slash is refactored
- some views are refactored by using Form, Form provides a more streamlined and user-friendly interface
- some data in some views are saved by using Swift´s *UserDefaults*

Some minor UI updates have been implemented, including enhanced headings in the Tasks section and Rsync parameters to enhance visual distinction. 

#### Tasks 

Within the Tasks section, the trailing slash option is refactored as follows:

- *Add trailing slash* - add a trailing slash to both the source and destination
- *Do not add trailing slash* - do not add a trailing slash, or if added, remove it
- *Do not check* - do not check for trailing slash or not on either the source or destination

Additionally, the values for the *Action* and *Trailing /* options are saved during the session if set to values other than the default. These values persist across Add, Update, and Profile changes. They are temporarily saved by *UserDefaults* and are reset to default values when RsyncUI restarts.

#### Home Catalog (Tasks) and Quick task

In both Home Catalogs and Quick task, the views have been refactored to utilize Form. Form provides a more streamlined and user-friendly interface. Additionally, data added within Quicktask is now saved by default by *UserDefaults*. When Quicktask is reentered, the data is automatically restored.

#### RsyncUI application icon

- The RsyncUI application icon has been updated using the new Icon Composer tool.
- This update supports icons in the new macOS Tahoe 26 and incorporates layered icons. The icon has also undergone a slight redesign, featuring a new cloud and numbers as layers in Icon Composer.