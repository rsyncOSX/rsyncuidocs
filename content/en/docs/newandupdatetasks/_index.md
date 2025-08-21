+++
author = "Thomas Evensen"
title =  "New tasks"
date = "2025-02-11"
tags = ["new tasks","profile"]
categories = ["synchronize"]
+++

A task requires a minimum of a local directory, the source, and a remote directory, the destination.

{{< alert color="warning" >}}

Always verify the result of a new task before executing. Select the *"Verify tasks"* from the primary Sidebar menu.

{{< /alert >}}

Pressing the `Enter` key will advance to the next field. Pressing the `Enter` key will automatically add a new task after the last input. Tasks are saved to permanent storage after each entry.

{{< figure src="/images/add/add.png" alt="" position="center" style="border-radius: 8px;" >}}

### Delete Tasks

Select the tasks you wish to delete and delete them from the Edit menu or by pressing the `backspace` button.

{{< figure src="/images/add/delete.png" alt="" position="center" style="border-radius: 8px;" >}}

### Data about Tasks

The following data pertains to tasks:

##### Action

- *synchronize* - default action for synchronize data from a *source* to a *destination*
- *snapshot* - saves changes and deletions prior to a synchronize operation
- *syncremote* - synchronize data from a remote *source* to a *local* folder
    - when adding a `syncremote` action, add the *local folder first* and the *remote folder as second*, RsyncUI will do the flip

##### Folder Parameters

- *Source folder* - required field
- *Destination folder* - required field

##### Trailing /

- *Add trailing slash* - add a trailing slash to both the source and destination
- *Do not add trailing slash* - do not add a trailing slash, or if added, remove it
- *Do not check* - do not check for trailing slash or not on either the source or destination

##### Synchronize ID

- *Synchronize ID* - informal tag for the task

##### Remote Parameters

- *Remote username* -  username for login to the remote server
- *Remote server* - either server name or IP address for the remote server

### Copy and Paste Tasks

Shortcuts for copy and paste are `⌘C` and `⌘V`, or from the Edit menu. The copy and paste operation creates a copy of the selected tasks and marks them with the "copy" status. The copied tasks retain all parameters.

