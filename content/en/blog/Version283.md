+++
author = "Thomas Evensen"
title = "Version 2.8.3"
date = "2025-12-16"
tags = ["changelog","version 2.8.3"]
categories = ["changelog"]
+++

### Version 2.8.3 (build 174) - not yet released

The version 2.8.3 will be released as a maintenance release in a few weeks.

The work on linting issues continues, and only a few remaining. A user-selected verification of default parameters such as `--delete` has been added. If the `--delete` parameter is included, the verification simply checks its presence. Other default parameters include `--archive` and `--compress`. The `--archive` parameter is always enabled, while the `--compress` parameter is only applicable for remote tasks.

The user can toggle validation on or off, with the default setting being on. This configuration will be saved to the user settings.

Additionally, unused properties have been removed from the task itself. The required parameters are automatically added by the SPM RsyncArguments.

