+++
author = "Thomas Evensen"
title = "Version 2.5.2"
date = "2025-05-14"
tags = ["changelog","version 2.5.2"]
categories = ["changelog"]
+++

### Version 2.5.2 (build 144) - May 14, 2025

{{< alert >}}

There has been *a lot of* UI-updates and cleanups of the UI within the latest release.  There are no changes to the model part or the process part, except for the schedule function which is new.

Recently, I encountered an unusual hang issue with RsyncUI, characterized by a spinning beach ball effect that caused RsyncUI to freeze. Yesterday, I was able to identify the specific cause and location of the problem, although the underlying reason remains unknown.

By simply commenting out a single line of code, I can reproduce the hang. I have attempted to pinpoint the cause using Xcode, but Xcode remains silent and does not generate any errors. While I suspect a potential bug in SwiftUI, the most significant achievement is that I have successfully recreated the hang and identified the precise code fix.

{{< /alert >}}

Major updates in the this release are, a detailed changelog on the GitHub release page:

- a fix for the above mentioned spinning beach ball
- the Verify Remote is now **not** enabled by default, enable in User settings
  - the Verify Remote function is slightly changed as well
  - please read about the function in section Verify Remote 
- update changes in User settings is now manual update, the automated save settings when changed did not work 100%
- there is a new view for Verify Tasks
    - the verify buttons, play icon, in Tasks and Rsync parameters are removed
    - the new view is very explicit about dry-run parameter is enabled
- German and Norwegian localization are deleted
    - regrettably, due to my limited proficiency in German, I am unable to provide a comprehensive translation in German. From this version, RsyncUI speaks English only
- the Tasks view is cleaned up, new help button for info add and delete the --delete parameter to rsync
    - add or delete, by default not added when new tasks
- the Rsync parameters view is cleaned up, new help button for info add and delete the --delete parameter to rsync
- the annoying popup when adding SSH-keys in Tasks and SSH-settings are removed and replaced
    - the values added are marked red text until values are compliant with validated input
    - example, if you add like `22d` in SSH port number, the text is marked red until the letter `d` is removed
- a new calendar for schedule actions, please read about the scheduler below before commence using it
    - to delete a schedule, just select it and press the back space button

{{< alert >}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."*  The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 

Its primary function is to automate selected synchronization of tasks as long as RsyncUI is alive. It *may* prove useful for users who require scheduled  synchronization of data during work.  RsyncUI may be minimized or not the active window and the timer will still work. But if you leave your Mac and it goes to sleep, the timer will not work.

{{< /alert >}}
