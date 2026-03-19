+++
author = "Thomas Evensen"
date = "2025-01-30"
title =  "Signing and notarization"
tags = ["notarize","signing"]
categories = ["general information"]
+++

RsyncUI is digitally signed with my Apple Developer Certificate and [notarized](https://support.apple.com/en-us/HT202491) by Apple. This verification ensures the application is free from malicious code and works with Gatekeeper. When opening a new or updated app for the first time, Apple will display a notification.

### What this means for you

- **Gatekeeper** will allow RsyncUI to run without warnings, because Apple has verified the developer signature.
- **No quarantine prompt** — you will not be asked to confirm that you want to open a downloaded app from an unknown developer.
- The SHA-256 hash published with each release lets you independently verify that the downloaded binary matches what was signed and notarized.

If installed via Homebrew, the hash is verified automatically. For direct downloads from GitHub, verify the hash manually before running the app.
