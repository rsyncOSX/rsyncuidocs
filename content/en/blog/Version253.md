+++
author = "Thomas Evensen"
title = "Version 2.5.3"
date = "2025-05-14"
tags = ["changelog","version 2.5.3"]
categories = ["changelog"]
+++

### Version 2.5.3 (build 145) - May 14, 2025

Major updates in the this release are, a detailed changelog on the GitHub release page. And thanks very much to [Johnny Sauce](https://github.com/sashemi) for valuable input and feedback.

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
- the annoying popup adding your own path for rsync and restore path is also removed and replaced with red text until validated OK
- a new calendar for schedule actions, please read about the scheduler below before commence using it
    - to delete a schedule, just select it and press the back space button
