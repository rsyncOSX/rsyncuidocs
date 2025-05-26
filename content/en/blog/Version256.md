+++
author = "Thomas Evensen"
title = "Version 2.5.6"
date = "2025-05-26"
tags = ["changelog","version 2.5.6"]
categories = ["changelog"]
+++

### Version 2.5.6 (build 148) - May 26, 2025 a development release

Almost every day I do some development in RsyncUI. The development are motivated by:

- issues and feedback from users
    - reporting issues and feedback is important
    - I am not an UX designer and I need feedback on the UI part when users find the UI difficult to use and understand
- updating the UI when I discover parts which, in my opinion, need to be changed
- fixing minor bugs, like the bug for profile picker below
- reading blogs about SwiftUI and Swift which make me do some refactor of code
- refactor old code

The development builds maintain the same version number while updating the build number. The changelog will meticulously document changes and the corresponding build numbers. Eventually, the development will be released as a new version later this summer. 

Build 148, May 26:

- fixed updating profile picker when RsyncUI discover new mounts and automatically loads profile
    - within the released version the profile picker does not show the correct profile loaded
    - the correct profile is actually loaded
- removed the weekly option from Calendar, only once and daily are schedule options
- within the Verify remote view, changed the toggle for delete parameter in pull and push
    - when choosing either pull or push, the delete parameter is included as deafult