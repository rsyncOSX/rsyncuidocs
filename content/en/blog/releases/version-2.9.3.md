+++
author = "Thomas Evensen"
title = "Version 2.9.3"
date = "2026-03-16"
tags = ["changelog","version 2.9.3"]
categories = ["changelog"]
+++

### Version 2.9.3 - March 16, 2026 (prerelease)

> If no bugs are reported during this week, this release will be released without a new build.

This prerelease addresses a logical error in the Tasks menu when selected from the sidebar. The Add tasks button on the toolbar is now consistently visible when in the Tasks menu. 

In version 2.9.2, the “Add tasks” button on the toolbar is only visible when a task is selected and when the “Edit” tab is selected.

Additionally, this release introduces two builds: one exclusively for Apple Silicon (arm86) and the other for both Apple Silicon and Intel architectures. The arm86 build is approximately 2MB smaller than the standard build.