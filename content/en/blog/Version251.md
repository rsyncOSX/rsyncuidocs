+++
author = "Thomas Evensen"
title = "Version 2.5.1"
date = "2025-05-05"
tags = ["changelog","version 2.5.1"]
categories = ["changelog"]
+++

### Version 2.5.1 (build 143) -release candidate

{{< alert >}}

There are input from a user, see last on page. All input will be evaluated and a fix will be added as part of the developing the new release.

{{< /alert >}}

This will stay as a release candidate for some weeks. I need some feedback on the Calendar part before making it a release, most likely in beginning of June 2025.

Major updates in this rc are:

- a new calendar for schedule actions, please read about the scheduler below before commence using it
    - to delete a schedule, just select it and press the back space button
- German and Norwegian localization are deleted
- the Verify a remote function is slightly changed

The scheduler is an easy to use and simple timer based trigger for synchronize data. The synchronize of data is triggered by the same method, URL-action, as for executing a synchronize data either by Widget or by external URL.

{{< alert >}}

The scheduler is implemented by using the Timer library, quote Apple: *"A timer that fires after a certain time interval has elapsed, sending a specified message to a target object."*  The timer has a strong reference to the run loop on the main thread. That also means that if the application goes to sleep, so does the run loop. And the timer is only active as long as RsyncUI is active. 

Its primary function is to automate selected synchronization of tasks as long as RsyncUI is alive. It *may* prove useful for users who require scheduled  synchronization of data during work. 

RsyncUI may be minimized or not the active window and the timer will still work. But if you leave your Mac and it goes to sleep, the timer will not work.

{{< /alert >}}

The Norwegian and German localization are also been deleted from this version. Regrettably, due to my limited proficiency in German, I am unable to provide a comprehensive translation in German. From this version, RsyncUI speaks English only. 

{{< figure src="/images/251/calendar.png" alt="" position="center" style="border-radius: 8px;" >}}

### Input from a user

Below are valuable input from a user. All input will be evaluated and corrected as part of making a new release in June 2025. There are more inputs, and I will read and add more inputs as I read through them. Additionally, every fix in the code will have a comment below every input.

1. It isn't clear what the tool does with Catalogs with spaces in the name. If I add escapes (\\), then the Estimation and Verification tasks freak out because they apparently run their commands with the directory enclosed in quotes. But the Rsync parameters interface does not show quotes around the directory name, and the rsync command should fail as shown.
2. If I put double quotes around the directory name under Tasks, then for some reason the tool adds a trailing / even if this option is turned off for the Task (and the option is uneditable after the task is created, and undiscernible in Dark mode - that is, it's impossible to tell what you chose just by looking at the greyed out checkbox). 2. With 1 and 2 in mind, I am not able to identify why a "synchronization" task passes both Estimate and Verify tasks, but a syncremote task passes Estimate but fails Verify due to rsync errors. I'm also not able to determine where do I find the rsync errors from the Verify action? Are they in a log somewhere? 
3. What are we supposed to do for synchronization vs syncremote? Should we flip the directories or not under "Tasks"? If I don't flip them, the rsync command with the user and IP does not produce correctly.
    1. This is **fixed**, in current release the Catalog parameters are flipped by RsyncUI - the fix now does the flipping hided for the user. Within the Tasks view
    2. Local Catalog is **always** the **first Catalog** in Tasks view
    3. Remote Catalog is **always** the **second Catalog** in Tasks view
    4. A syncremote pull data from a remote which require that Catalog parameters compared to a normal synchronize task are flipped. RsyncUI now flip this catalog hided for the user.
4. It is not clear that --dry-run is automatically imposed IF I don't hit "play", but it is excluded if I hit "play". Grok had to explain it to me. There's a neato "--dry-run" toggle under Restore, and I wonder why you didn't implement that for the main sync tool sections.
5. Why are the backup switch and SSH parameter options tied together with a toggle? Why does the SSH parameter need a switch at all, and it doesn't seem like the switch affects the SSH parameter or the port.
6. Why do I need to "hack" extra SSH options in the task specific SSH field? (such as -o StrictHostKeyChecking=no) It's especially confusing since that field appears to have an annoying validation when you first start typing in it (a modal popup).
7. Please consolidate the logs in one place. There is a log button in Synchronize that leads to a window where latest updates are at the bottom and have to be scrolled down to. Also this log just smashes together output for all Tasks, and doesn't separate by Tasks. There's no log for Verify or Estimate. Every flow should just have a log so that we can troubleshoot rsync responses, as well as what the file sync actions or determinations are.
8. Why would the "Don't add /" be non-editable for Tasks after they are created? I understand the decision behind keeping sync/syncremote non editable after create.
9. Confirm Execute should be a default on, imo.
10. Instead of popups, possibly you could look to web forms as an inspiration. Fields that don't "validate" could be marked with a red border, and maybe even a small note underneath (like "this needs to be formatted starting with ~/". As long as fields don't validate, then the "submit" type actions would not proceed.




