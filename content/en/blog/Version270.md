+++
author = "Thomas Evensen"
title = "Version 2.7.0"
date = "2025-08-31"
tags = ["changelog","version 2.7.0"]
categories = ["changelog"]
+++

### Version 2.7.0 (build 161) - not yet released

The next version, 2.7.0 build 161, will be released after macOS Tahoe 26 is released. Currently, there are no plans to add any macOS Tahoe 26-specific features, such as Liquid Glass properties for buttons. The next version will be compiled with Xcode 26 on macOS Tahoe 26 and will adapt any default UI settings by the running version of macOS. However, there may be some macOS Tahoe 26-specific properties in future version 2.7.x of RsyncUI.

#### Charts

The log records of RsyncUI store the date, number of files transferred, seconds to transfer, and the amount of data transferred in MB. All data is retrieved from the output of rsyncUI. While it is uncertain whether any charts of this data are of interest, I have begun testing data extraction and presenting some charts. Currently, if more than one transfer occurs in a day, only the transfer with the most files is selected for that day. Similarly, the amount of data is selected. Additionally, it will be possible to present only the 20 or any other number of dates with the most files or the most data from the entire dataset.

As development is still in its early stages, I welcome any ideas you may have. Please feel free to contact me via email thomeven@gmail.com.

{{< figure src="/images/v270/chart.png" alt="" position="center" style="border-radius: 8px;" >}}

Some multiple dates, select date where number of files is greatest.

{{< figure src="/images/v270/barfiles.png" alt="" position="center" style="border-radius: 8px;" >}}

Some multiple dates, select date where size of transfer is greatest.

{{< figure src="/images/v270/barsize.png" alt="" position="center" style="border-radius: 8px;" >}}

#### JottaUI

 have also commenced developing a graphical user interface (GUI), JottaUI, on top of the Norwegian company JottaCloud's command-line tool, jotta-cli. JottaCloud is a cloud storage provider, and by utilizing the jotta-cli to configure and enable backup and synchronization of data, we can enhance the user experience. The JottaUI application presents the status of data transfers, allows users to add catalogs for backup and synchronization, view log files, and perform other relevant tasks. Its primary purpose is to provide users with easy-to-follow status updates and the ability to trigger updates. The application is currently available in English only.

If you are interested in testing the application, please do not hesitate to contact me via email at thomeven@gmail.com. The JottaUI will be signed and notarized, similar to RsyncUI.

{{< figure src="/images/v270/status.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v270/json.png" alt="" position="center" style="border-radius: 8px;" >}}

{{< figure src="/images/v270/log.png" alt="" position="center" style="border-radius: 8px;" >}}
