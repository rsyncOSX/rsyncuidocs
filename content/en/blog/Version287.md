+++
author = "Thomas Evensen"
title = "Version 2.8.7"
date = "2026-01-10"
tags = ["changelog","version 2.8.7"]
categories = ["changelog"]
+++

### Version 2.8.7 - Jan 10, 2026 dev build

I am releasing this as a development build for testing purposes. The two packages listed below are essential for the proper functioning of RsyncUI. The updated package should resolve the issue “no stats”.

<div class="alert alert-danger" role="alert">

It appears that the updated package fulfills its intended purpose. I have not encountered the "no stats" issue after the update, and several users have downloaded it. For the time being, it will remain a release candidate. However, without a new build, it will become the next release if no issues are reported.

It is anticipated that it will become the next release in approximately one week. 

</div>

In contrast to version 2.8.6, this development build introduces only two updates: an updated [package RsyncProcessStreaming](https://github.com/rsyncOSX/RsyncProcessStreaming) and a function in [package ParseRsyncOutput](https://github.com/rsyncOSX/ParseRsyncOutput) that writes debug data to a text file if the “no stats” issue occurs.

For further details about RsyncProcessStreaming, please refer to the following document:

- a [Code Quality Report](https://github.com/rsyncOSX/RsyncUI/blob/main/QUALITY_ANALYSIS_DETAILED.md)

Additionally, there is a fixed issue with the command strings for `Copy public SSHKey` and `Verify Public SSHKey` within the “Verify Tasks” menu. The issue is that the command displayed also adds the keygen command in front of the command. 
