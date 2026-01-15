+++
author = "Thomas Evensen"
title = "Version 2.8.7"
date = "2026-01-14"
tags = ["changelog","version 2.8.7"]
categories = ["changelog"]
+++

### Version 2.8.7 - Jan 14, 2026

<div class="alert alert-danger" role="alert">

It appears that the updated package successfully addresses the issue of missing statistics. I have not encountered the “no stats” problem after the update, and several users have downloaded the release candidate. The release candidate has now been released as the new release without a new build.

</div>

In contrast to version 2.8.6, this release introduces only two updates: an updated [package RsyncProcessStreaming](https://github.com/rsyncOSX/RsyncProcessStreaming) and a function in [package ParseRsyncOutput](https://github.com/rsyncOSX/ParseRsyncOutput) that writes debug data to a text file if the “no stats” issue occurs.

Additionally, there is a fixed issue with the command strings for `Copy public SSHKey` and `Verify Public SSHKey` within the “Verify Tasks” menu. The issue is that the command displayed also adds the keygen command in front of the command. 

For additional information regarding RsyncUI’s Swift Packages, kindly refer to the accompanying document.

- a [Code Quality Report](https://github.com/rsyncOSX/RsyncUI/blob/main/QUALITY_ANALYSIS_DETAILED.md)

### Rsync Verify

In the coming days, I will release a release candidate for the new application, [RsyncVerify](https://github.com/rsyncOSX/RsyncVerify). This application replaces the functionality that was removed from RsyncUI. You can read about the application in the blog post titled “Verify remote.” The application includes parsing and tagging of each line of output. It is important to note that RsyncVerify is **not** a replacement for RsyncUI. The motivation for developing VerifyRemote is outlined in the blog post.