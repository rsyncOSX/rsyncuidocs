+++
author = "Thomas Evensen"
title = "Version 2.8.1"
date = "2025-12-05"
tags = ["changelog","version 2.8.1"]
categories = ["changelog"]
+++

### Version 2.8.1 (build 172) - Dec 5, 2025

An AI-generated changelog is available at the bottom of this page.

This maintenance release addresses a few issues. 

All annoying messages regarding missing files are resolved.

## Empty stats file

Please see the note about *no stats* in the changelog (blog) for version 2.8.0.

<div class="alert alert-danger" role="alert">
The alert is *currently disabled by default in version 2.8.1*. 

However, version 2.8.2 will introduce an option to enable it. If RsyncUI detects an empty statistics file, it will append a default log record stating `0 files : 0.00 MB in 0.00 seconds`.

</div>

If logging fails due to the aforementioned reason, this error will be generated, if *enabled in version 2.8.2*.

{{< figure src="/images/gettingstarted/nostats.png" alt="" position="center" style="border-radius: 8px;" >}}
