+++
author = "Thomas Evensen"
title = "URL commands"
date = "2025-02-10"
tags = ["url commands","deep links","synchronize","widget"]
categories = ["advanced features"]
+++

Deep links provide direct access to app features via URL. Using deep links, you can estimate and synchronize in a single click. Deep links in RsyncUI group actions that typically require multiple steps.

There are three methods of using deep links:

- enable RsyncUI widgets
- use URL functions direct within RsyncUI
- save an URL-link in e.g. Notepad

#### RsyncUI Widget

One widget is embedded in RsyncUI:

- *estimating and synchronizing*

The widget retrieves a saved URL from storage. In the Tasks view, there is a URL view where you can save the required URL. The widget shows whether a validated URL is present. To enable the widget on macOS, click the date and time icon in the upper right corner of your screen. Edit widgets and select RsyncUI, then add the widget.

After enabling the widget, a single click on the widget will launch RsyncUI and execute the corresponding action. To modify the URL, update and save the new URL.

#### Execute URL´s from within RsyncUI

Deep links also enable automation of actions within RsyncUI. A single click on the toolbar icon executes  the URL  action. RsyncUI generates the necessary URL based on the loaded profile and the required action. The two yellow toolbar icons allow execution of URL commands from within RsyncUI, as demonstrated in section above.

{{< figure src="/images/url/urlcommand.png" alt="" position="center" style="border-radius: 8px;" >}}

#### URLs and Notepad

URLs must start with `rsyncuiapp://`:

| Action                                             | URL                                                                     |
|----------------------------------------------------|-------------------------------------------------------------------------|
| Estimate all tasks, automatically synchronize data | `rsyncuiapp://loadprofileandestimate?profile=Pictures`                  |

- *Estimate all tasks and automatically synchronize data*
  - load profile, estimate all tasks and automatically synchronize data

#### View URL

You can copy the correct URLs and save them in an application like Notepad for easy access to start a synchronization task. 

#### Errors in URL link

If RsyncUI encounters an invalid URL link, it will generate errors. Only well-defined URLs (specifically those supported by RsyncUI) are processed and executed. All URLs are validated as valid, but only defined URLs for RsyncUI are actually executed.
