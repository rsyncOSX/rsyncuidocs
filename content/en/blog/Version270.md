+++
author = "Thomas Evensen"
title = "Version 2.7.0"
date = "2025-09-03"
tags = ["changelog","version 2.7.0"]
categories = ["changelog"]
+++

### Version 2.7.0 (build 161) - release candidate

The next version, 2.7.x build 16x, will be released **after** macOS Tahoe 26 is released. 

Currently, there are no plans to add any macOS Tahoe 26-specific features, such as Liquid Glass properties for buttons. The next version will be compiled with Xcode 26 on macOS Tahoe 26 and will adapt any default UI settings by the running version of macOS. However, there may be some macOS Tahoe 26-specific properties in future version 2.7.x of RsyncUI.

#### Charts

Development is progressing.

The log records of RsyncUI store the date, number of files transferred and the amount of data transferred in MB. All data is retrieved from the output of rsyncUI. While it is uncertain whether any charts of this data are of interest, I have begun testing data extraction and presenting some charts. As development is still in its early stages, I welcome any ideas you may have. Please feel free to contact me via email thomeven@gmail.com.

{{< figure src="/images/v270/chart.png" alt="" position="center" style="border-radius: 8px;" >}}

Some multiple dates, select date where number of files is greatest.

{{< figure src="/images/v270/barfiles.png" alt="" position="center" style="border-radius: 8px;" >}}

Some multiple dates, select date where size of transfer is greatest.

{{< figure src="/images/v270/barsize.png" alt="" position="center" style="border-radius: 8px;" >}}

In bar charts, selecting a row in the data table highlights the corresponding row in the chart.

{{< figure src="/images/v270/selectbardata.png" alt="" position="center" style="border-radius: 8px;" >}}
