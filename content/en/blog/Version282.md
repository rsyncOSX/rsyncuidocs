+++
author = "Thomas Evensen"
title = "Version 2.8.2"
date = "2025-12-14"
tags = ["changelog","version 2.8.2"]
categories = ["changelog"]
+++

### Version 2.8.2 (build 173) - Dec 14, 2025

This version has undergone numerous linting updates. Additionally, a bug related to enabling or disabling the `—delete` parameter has been resolved. Furthermore, a user settings flag for enabling or disabling the `Silence missing stats` parameter, which generates an error if the summarized stats file is empty.

As part of my ongoing experimentation with Visual Studio Code (VSC) and the GitHub MCP services for direct integration with GitHub Copilot (AI), several code updates have been made. The majority of these updates are attributed to the implementation of additional SwiftLint rules. VSC has proven to be an effective tool for identifying and resolving linting issues and updating code.

From this version, VSC has become an integral part of my development tools for the RsyncUI project. While Xcode 26 remains my primary development environment, all release builds, including notifications and signing, are executed via command line and a Makefile.

The primary supporting tools include:

- [SwiftLint](https://github.com/realm/SwiftLint): Utilized for code quality assurance.
- [SwiftFormat](https://github.com/nicklockwood/SwiftFormat): Employed for code formatting.
- [periphery](https://github.com/peripheryapp/periphery): Utilized to eliminate unused code.

All of these tools are widely recognized and utilized by numerous developers.

The periphery application is specifically designed to eliminate unused code. SwiftFormat is utilized for code formatting, while SwiftLint ensures code quality. All instructions for SwiftFormat within the code have been removed, and both tools now share a single configuration file containing their respective instructions. This integration has proven to be highly effective.
