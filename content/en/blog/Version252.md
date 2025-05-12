+++
author = "Thomas Evensen"
title = "Version 2.5.2"
date = "2025-05-12"
tags = ["changelog","version 2.5.2"]
categories = ["changelog"]
+++

### Version 2.5.2 (build 144) - release candidate

{{< alert >}}

There has been several UI-updates and cleanups of the UI within the latest release candidate. See blog "Input from User"

{{< /alert >}}

Major updates in the new **updated** release candidate May 12, 2025. This is most likely last release candidate before a new release.

- a new calendar for schedule actions, please read about the scheduler below before commence using it
    - to delete a schedule, just select it and press the back space button
- the Verify Remote is now **not** enabled by default, enable in User settings
  - the Verify Remote function is slightly changed as well
    - please read about the function in section Verify Remote 
- update changes in User settings is now manual update, the automated save settings when changed did not work 100%
- there is a new view for Verify Tasks
    - the verify buttons, play icon, in Tasks and Rsync parameters are removed
    - the new view is very explicit about dry-run parameter is enabled
- German and Norwegian localization are deleted
    - Regrettably, due to my limited proficiency in German, I am unable to provide a comprehensive translation in German. From this version, RsyncUI speaks English only. 
- the Tasks view is cleaned up, new help button for info add and delete the --delete parameter to rsync
    - add or delete, by default not added when new tasks
- the Rsync parameters view is cleaned up, new help button for info add and delete the --delete parameter to rsync
- the annoying popup when adding SSH-keys in Tasks and SSH-settings are removed and replaced
    - the values added are marked red text until values are compliant with validated input
    - example, if you add like `22d` in SSH port number, the text is marked red until the letter `d` is removed

{{< alert >}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."*  The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 

Its primary function is to automate selected synchronization of tasks as long as RsyncUI is alive. It *may* prove useful for users who require scheduled  synchronization of data during work.  RsyncUI may be minimized or not the active window and the timer will still work. But if you leave your Mac and it goes to sleep, the timer will not work.

{{< /alert >}}
