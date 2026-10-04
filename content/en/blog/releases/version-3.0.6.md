+++
author = "Thomas Evensen"
title = "Version 3.0.6 — Release Candidate"
date = "2026-10-04"
tags = ["changelog","version 3.0.6"]
categories = ["changelog"]
+++

# RsyncUI 3.0.6 — Release Candidate

<div class="alert alert-secondary" role="alert">

Version 3.0.6 is available as a release candidate for testing. It has not yet been released as a stable version. This candidate improves rsync error reporting and respects the configured preference for checking errors in rsync output.

</div>

Changes since `v3.0.5`, based on the `version-3.0.6` branch through commit `05c4752d` (September 30, 2026).

## 🐛 Error reporting fixes

- Fixed rsync output error checking so it follows the user's configured preference instead of always being enabled.
- Improved failure alerts to include the rsync exit code and a concise summary of standard error output.
- Limited the output shown in failure alerts to ten lines, keeping alerts manageable even when rsync produces large amounts of output.
- Preserved the most recent line containing “error” when it would otherwise fall outside the displayed summary.

## 🧪 Regression coverage

- Added tests for large multiline error output, error messages across multiple output chunks, and short or empty output.
- Added tests for failure-alert presentation and for enabling or disabling rsync output error checking.

## 📦 Version information

- Updated the application and widget version to `3.0.6`.
- Updated the application and widget build number from `208` to `209`.
