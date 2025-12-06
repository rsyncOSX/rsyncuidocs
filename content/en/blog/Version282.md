+++
author = "Thomas Evensen"
title = "Version 2.8.2"
date = "2025-12-06"
tags = ["changelog","version 2.8.2"]
categories = ["changelog"]
+++

### Version 2.8.2 (build 173) - not yet released

I have commenced a comprehensive code formatting cleanup utilizing [SwiftLint](https://github.com/realm/SwiftLint), [SwiftFormat](https://github.com/nicklockwood/SwiftFormat), and [periphery](https://github.com/peripheryapp/periphery). Despite using these tools for several years, some cleanup was still required. 

The periphery application is employed to eliminate unused code. SwiftFormat is utilized for code formatting and SwiftLint code quality. All instructions for SwiftFormat in code are removed, and both tools now have a single configuration file each containing instructions. They work very well together.

As a result, numerous code modifications have been made, primarily due to the formatting adjustments implemented using the aforementioned tools.

All of these tools are widely recognized and utilized by numerous developers. 

Additionally, there will be some code refactoring, which will be informed about later in December 2025.