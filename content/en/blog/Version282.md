+++
author = "Thomas Evensen"
title = "Version 2.8.2"
date = "2025-12-06"
tags = ["changelog","version 2.8.2"]
categories = ["changelog"]
+++

### Version 2.8.2 (build 173) - not yet released

I have commenced a comprehensive code formatting cleanup utilizing [SwiftLint](https://github.com/realm/SwiftLint), [SwiftFormat](https://github.com/nicklockwood/SwiftFormat), and [periphery](https://github.com/peripheryapp/periphery). Despite using these tools for several years, some cleanup was still required. 

All of the aforementioned tools are widely recognized and utilized by numerous developers. 

The periphery application is employed to eliminate unused code. SwiftFormat is utilized for code formatting and SwiftLint code quality. All instructions for SwiftFormat in code are removed, and both tools now have a single configuration file each containing instructions. They work very well together.

As a result, numerous code modifications have been made, primarily due to the formatting adjustments implemented using the aforementioned tools.

### Visual Studio Code and GitHub MCP services

Model Context Protocol (MCP) is an open standard, introduced in November 2024 by Anthropic. Quote Google *"The Model Context Protocol (MCP) is an open standard designed to solve this. Introduced by Anthropic in November 2024, MCP provides a secure and standardized "language" for LLMs to communicate with external data, applications, and services. It acts as a bridge, allowing AI to move beyond static knowledge and become a dynamic agent that can retrieve current information and take action, making it more accurate, useful, and automated."*

I have recently begun utilizing Visual Studio Code (VSC) and its integration with GitHub MCP services. I initiated a request to VSC, utilizing the MCP services, to analyze the codebase for RsyncUI and identify issues in naming conventions. I am highly impressed by the capabilities of AI in supporting developers. The aforementioned request resulted in several code updates, and two reports have been generated as a result. These reports are authored by AI and are accessible from the root directory of the RsyncUI repository.