+++
author = "Thomas Evensen"
title = "Version 2.9.0"
date = "2026-01-20"
tags = ["changelog","version 2.9.0"]
categories = ["changelog"]
+++

### Version 2.9.0 - Jan 20, 2026 release candidate

The development of the next version has commenced. Currently, a few enhancements have been implemented in this version. The version is scheduled for release by the end of January. It is likely that more updates will be committed in the future.

In addition, there have been several linting updates. Only a few linting issues remain, all linting rules have been deleted from the code, and there is now only one `.swiftlint.yml` file containing all rules for all code.

- Tagging of output from rsync, refer to the blog post titled "[Verify Remote](https://rsyncui.netlify.app/blog/2026/01/15/verify-remote/)" for more info about the tagging. It is only the *tagging* within this blog which are relevant, not the function described in the post.
  - The tagging is depended upon two parameters for rsync
  - `--itemize-changes` and `--update`
  - It is important to note that rsync generates more output when parameters above are set. However, this does not imply that more data is being synchronized; it simply indicates that rsync is producing more output.
- In the Tasks menu, when using a *single table* for tasks, the "Use two tables Inspector" setting is disabled. Consequently, the Inspectors for Edit and Parameters are not closed when the tab is changed. Screenshots are provided below for reference.

For further details, please refer to the following documents:

- a detailed [Changelog](https://github.com/rsyncOSX/RsyncUI/blob/main/CHANGELOG.md)
- a [Code Quality Report](https://github.com/rsyncOSX/RsyncUI/blob/main/QUALITY_ANALYSIS_DETAILED.md)
