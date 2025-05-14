+++
author = "Thomas Evensen"
title = "Input from User"
date = "2025-05-01"
tags = ["changelog","issues"]
categories = ["issues"]
+++

### Input from user

{{< alert >}}

There is input from [Johnny Sauce](https://github.com/sashemi). 

{{< /alert >}}

Below are valuable input from a user. All input will be evaluated and corrected as part of making a new release in June 2025. There are more inputs, and I will read and add more inputs as I read through them. Additionally, every fix in the code will have a comment below every input.

#### Nr 1 - seems not to be an issue

It isn't clear what the tool does with Catalogs with spaces in the name. If I add escapes (\\), then the Estimation and Verification tasks freak out because they apparently run their commands with the directory enclosed in quotes. But the Rsync parameters interface does not show quotes around the directory name, and the rsync command should fail as shown.

- Using spaces **does not** requiere any special actions, RsyncUI accept spaces, it seems like rsync treats space like any other character.
- To create a Remote catalog with space on Debian requiere the following command : `mkdir Blackmagic\ Design`.
- The local Catalog also includes cataloges with space, the remote accepts spaces with no special actions.

{{< figure src="/images/251/space.png" alt="" position="center" style="border-radius: 8px;" >}}

The computed rsync command includes spaces, no escape characters needed. The only escape character needed is if you explicit are creating a destination catalog  on the Linux host including a space in catalog name. 

{{< figure src="/images/251/space2.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Nr 2 - updated

*If I put double quotes around the directory name under Tasks, then for some reason the tool adds a trailing / even if this option is turned off for the Task (and the option is uneditable after the task is created, and undiscernible in Dark mode - that is, it's impossible to tell what you chose just by looking at the greyed out checkbox). 2. With 1 and 2 in mind, I am not able to identify why a "synchronization" task passes both Estimate and Verify tasks, but a syncremote task passes Estimate but fails Verify due to rsync errors. I'm also not able to determine where do I find the rsync errors from the Verify action? Are they in a log somewhere?*

- Double quotes are not allowed in catalog names, they are now removed in code
- RsyncUI does ALLOW spaces in catalognames, no need for either double quote or escape character
- manually creating a catalog on a remote Linux server requiere using escape character

Need some development to take care of the trailing "/", should be able to remove it by update.

#### Nr 3 - updated

*What are we supposed to do for synchronization vs syncremote? Should we flip the directories or not under "Tasks"? If I don't flip them, the rsync command with the user and IP does not produce correctly.*

- This is **fixed**, in current release the Catalog parameters are flipped by RsyncUI - the fix now does the flipping hided for the user. Within the Tasks view
- Local Catalog is **always** the **first Catalog** in Tasks view
- Remote Catalog is **always** the **second Catalog** in Tasks view
- A syncremote pull data from a remote which require that Catalog parameters compared to a normal synchronize task are flipped. RsyncUI now flip this catalog hided for the user.

#### Nr 4 - updated 

*It is not clear that --dry-run is automatically imposed IF I don't hit "play", but it is excluded if I hit "play". Grok had to explain it to me. There's a neato "--dry-run" toggle under Restore, and I wonder why you didn't implement that for the main sync tool sections.*

- There is a **new view** for Verify task, the play button is removed from both Tasks and Rsync parameters view. The new view is also state clearly an estimate includes --dry-run.
- Adding a --dry-run toggle for the main synchronize tasks is not possible, please read the section "Synchronize data". Executing tasks, either by shortcut, by magic wand on toolbar ALWAYS start with an estimation run, requiered to make the progress bar work

#### Nr 5 - updated

*Why are the backup switch and SSH parameter options tied together with a toggle? Why does the SSH parameter need a switch at all, and it doesn't seem like the switch affects the SSH parameter or the port.*

- The view is cleaned up and the Backup switch is moved
- There is also a new help button about the --delete parameter, 

#### Nr 6 - investigating needed

*Why do I need to "hack" extra SSH options in the task specific SSH field? (such as -o StrictHostKeyChecking=no) It's especially confusing since that field appears to have an annoying validation when you first start typing in it (a modal popup).*

I need to investigate this issue. I will change to Alert, modal popup, but the parameters are originally only for user selected SSH-key and SSH-port number. I will investiate if possible to add other SSH options, and the modal popup will be changed.

#### Nr 7 - no updates needed

*Please consolidate the logs in one place. There is a log button in Synchronize that leads to a window where latest updates are at the bottom and have to be scrolled down to. Also this log just smashes together output for all Tasks, and doesn't separate by Tasks. There's no log for Verify or Estimate. Every flow should just have a log so that we can troubleshoot rsync responses, as well as what the file sync actions or determinations are.*

RsyncUI only create log records AFTER a sucessfull synchronization of data. It is not possible to store *every* output from rsync, output from rsync might be huge. And by any command in RsyncUI it is possibe to inspect to output from RsyncUI. If there are discovered errors in output, an error is thrown and the user can inspect the output.

The logview always presents the most recent logs at top, not bottom. When opening the view and there are more than one task, the view show all log records. Most recent logs at top.

{{< figure src="/images/251/alllogs.png" alt="" position="center" style="border-radius: 8px;" >}}

If a task is selected, only log records for that task is presented. Most recent at top.

{{< figure src="/images/251/selectedlogs.png" alt="" position="center" style="border-radius: 8px;" >}}

How to inspect the output from rsync by an estimate run. The view is presented as part of en estimation run, please read the documentation section "Synchronize data"

{{< figure src="/images/251/estimate.png" alt="" position="center" style="border-radius: 8px;" >}}

Selection a row presents the output from rsync. Blue numbers indicates there are data to be synchronized.

{{< figure src="/images/251/estimatedetails.png" alt="" position="center" style="border-radius: 8px;" >}}

#### Nr 8 - updated

*Why would the "Don't add /" be non-editable for Tasks after they are created? I understand the decision behind keeping sync/syncremote non editable after create.*

- The trailing "/" is fixed.
- If you have a synchronize action and want to flip it to a syncremote, you have to create a new task. 

#### Nr 9 - no updates 

*Confirm Execute should be a default on, imo.*

See answer to nr 4.

#### Nr 10 - updated

*Instead of popups, possibly you could look to web forms as an inspiration. Fields that don't "validate" could be marked with a red border, and maybe even a small note underneath (like "this needs to be formatted starting with ~/". As long as fields don't validate, then the "submit" type actions would not proceed.*

- The popus are removed, values are marked with red text until validated OK




