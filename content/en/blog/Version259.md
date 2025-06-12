+++
author = "Thomas Evensen"
title = "Version 2.5.9"
date = "2025-06-12"
tags = ["changelog","version 2.5.9"]
categories = ["changelog"]
+++

### Version 2.5.9 (build 153) - not yet released

This blog serves as a notification regarding the upcoming version of RsyncUI. 

The latest release, *version 2.5.8 b152* is *stable*. But very often, internal refactor, QA and cleaning of code causes more cleanup and refactors. And so far there has been several refactors and cleanups in code next version. The GitHub repository is updated. You may browse changes in code by view  [latest release](https://github.com/rsyncOSX/RsyncUI/releases/tag/v2.5.8). The main repository is committed with latest updates.

You may ask why are there refactors and cleanup? Almost every day. I spend some time review parts of my code. I get input by reading blogs and some blogs do inspire my to do some changes. One major objective is to get code which is effective, clean and easy to understand. And remove any code not used. There is a 20/80 rule, the Pareto principle, which suggest that approx 20% of the code accounts for 80% of the execution. What I am saying is, identify the most used code and make it as effective as possible. And not only effective, but easy to read and understand. 

RsyncUI does also heavily use the Apple Framework OSLog, for logging. The logging in RsyncUI produces logs at every major step. By using Xcode, I can observe every major step of what RsyncUI is doing. In total of about 17,8K lines of code there are 188 log statments in 55 files. 

There will be a more detailed changelog when next release is ready for release by end of June 2025. 

