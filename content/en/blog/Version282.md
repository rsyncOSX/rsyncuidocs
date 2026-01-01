+++
author = "Thomas Evensen"
title = "Version 2.8.2"
date = "2025-12-14"
tags = ["changelog","version 2.8.2"]
categories = ["changelog"]
+++

### Version 2.8.2 (build 173) - Dec 14, 2025

This release includes extensive linting updates. A bug related to toggling the `—delete` parameter is fixed. A new user setting controls `Silence missing stats`, which triggers an error if the summarized stats file is empty.

During ongoing experimentation with Visual Studio Code (VSC) and the GitHub MCP services for GitHub Copilot integration, I made several code updates. Most stem from adding SwiftLint rules. VSC has been effective for spotting and fixing lint issues.

From this version on, VSC is part of my toolchain. Xcode 26 remains the primary IDE, while release builds, signing, and notifications run via the command line and a Makefile.

The primary supporting tools include:

- [SwiftLint](https://github.com/realm/SwiftLint): code quality
- [SwiftFormat](https://github.com/nicklockwood/SwiftFormat): formatting
- [periphery](https://github.com/peripheryapp/periphery): unused-code detection

All are widely used tools.

Periphery removes unused code, SwiftFormat handles formatting, and SwiftLint enforces style and safety. Inline SwiftFormat directives were removed; both tools now share a single configuration file, which has worked well.
