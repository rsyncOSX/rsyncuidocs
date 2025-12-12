+++
author = "Thomas Evensen"
title = "Version 2.8.2 documents"
date = "2025-12-12"
tags = ["changelog","version 2.8.2"]
categories = ["changelog"]
+++

Some AI-generated documents about Version 2.8.2.

### Version 2.8.2 (build 173) - release candidate 2

<div class="alert alert-secondary" role="alert">
  
The plan is to release version 2.8.2 before Christmas. The detailed changelog is available on the release page on GitHub. A detailed summarized changelog is last on this page.

If no bugs are reported, the rc2 will become the next release version 2.8.2, and no new builds will be released. Therefore, please download and test the build.

</div>

As part of my ongoing experimentation with Visual Studio Code (VSC) and the GitHub MCP services for direct integration with GitHub Copilot (AI), several code updates have been made. The majority of these updates are attributed to the implementation of additional SwiftLint rules. VSC has proven to be an effective tool for identifying and resolving linting issues and updating code.

From this version, VSC has become an integral part of my development tools for the RsyncUI project. While Xcode 26 remains my primary development environment, all release builds, including notifications and signing, are executed via command line and a Makefile.

The primary supporting tools include:

- [SwiftLint](https://github.com/realm/SwiftLint): Utilized for code quality assurance.
- [SwiftFormat](https://github.com/nicklockwood/SwiftFormat): Employed for code formatting.
- [periphery](https://github.com/peripheryapp/periphery): Utilized to eliminate unused code.

All of these tools are widely recognized and utilized by numerous developers.

The periphery application is specifically designed to eliminate unused code. SwiftFormat is utilized for code formatting, while SwiftLint ensures code quality. All instructions for SwiftFormat within the code have been removed, and both tools now share a single configuration file containing their respective instructions. This integration has proven to be highly effective.


### Visual Studio Code (VSC) and GitHub MCP services

Model Context Protocol (MCP) is an open standard, introduced in November 2024 by Anthropic. Quote Google *"The Model Context Protocol (MCP) is an open standard designed to solve this. Introduced by Anthropic in November 2024, MCP provides a secure and standardized "language" for LLMs to communicate with external data, applications, and services. It acts as a bridge, allowing AI to move beyond static knowledge and become a dynamic agent that can retrieve current information and take action, making it more accurate, useful, and automated."*

I have recently begun utilizing Visual Studio Code (VSC) and its integration with GitHub MCP services. I initiated a request to VSC, utilizing the MCP services, to analyze the codebase for RsyncUI and identify issues in naming conventions. I am highly impressed by the capabilities of AI in supporting developers. The aforementioned request resulted in several code updates, and two reports have been generated as a result. These reports are authored by AI and are accessible from the root directory of the RsyncUI repository.

Although Xcode remains my primary development tool, Visual Studio Code (VSC) is also officially supported by [swift.org](https://www.swift.org/install/macos/). Utilizing Xcode ensures that the latest Swift toolchain is always up-to-date. VSC can also utilize the Xcode-installed toolchain, and it offers a wide range of extensions. 
