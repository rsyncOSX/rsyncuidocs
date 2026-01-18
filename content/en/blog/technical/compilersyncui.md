+++
author = "Thomas Evensen"
title = "Compiling RsyncUI"
date = "2026-01-16"
tags = ["compile"]
categories = ["technical details"]
+++

### Overview

<div class="alert alert-danger" role="alert">

There are at least three methods to compile RsyncUI, one without an Apple Developer account and two with an Apple Developer account. Regardless of the method used, it is straightforward to compile RsyncUI, as it is not dependent on any third-party code or library.

</div>

The easist method is by using the included Makefile. The default make in `/usr/bin/make` does the job. 

### Compile by make

If you have an Apple Developer account, you should open the RsyncUI project and replace the `Signing & Capabilities` section with your own Apple Developer ID before using `make` and the procedure outlined below.

The use of the make command necessitates the application-specific password. There are two commands available for use with make: one creates a release build exclusively for RsyncUI, while the other generates a signed version that includes a DMG file.

If only utilizing the `make archive` command did not necessitate the application-specific password, it would suffice to update only the `Signing & Capabilities` section. It is highly probable that the `make archive` command will still function even if set to `Sign to Run Locally`.

To create a DMG file, the make command is dependent on the [create-dmg](https://github.com/create-dmg/create-dmg) tool. The instructions for create-dmg are included in the Makefile. Ensure that the fork of create-dmg is on the same level as the fork of RsyncUI. Before using make, create and store an app-specific password.

The following procedure creates and stores an app-specific password:

1. Visit appleid.apple.com and log in with your Apple ID.
2. Navigate to the Sign-In and Security section and select App-Specific Passwords → Generate an App-Specific Password.
3. Provide a label to help identify the purpose of the password (e.g., notarytool).
4. Click Create. The password will be displayed once; copy it and store it securely.

After creating the app-specific password, execute the following command and follow the prompts:

`xcrun notarytool store-credentials --apple-id "youremail@gmail.com" --team-id "A1B2C3D4E5"`

- Replace `youremail@gmail.com` and `A1B2C3D4E5` with your actual credentials.

Name the app-specific password  `RsyncUI` (in appleid.apple.com) and set `Profile name: RsyncUI` when executing the above command.

The following dialog will appear:

```
This process stores your credentials securely in the Keychain. You reference these credentials later using a profile name.

Profile name:
RsyncUI
App-specific password for youremail@gmail.com: 
Validating your credentials...
Success. Credentials validated.
Credentials saved to Keychain.
To use them, specify `--keychain-profile "RsyncUI"`
```

Following the above steps, the following make commands are available from the root of RsyncUI's source catalog:

- `make` - will generate a signed and notified DMG file including the release version of RsyncUI.
- `make archive` - will produce a release version, removing all debug information, without signing within the `build` catalog.
- `make clean` - will delete all build data.

### Compile by Xcode

If you have an Apple Developer account, use your Apple Developer ID in Xcode.

#### Apple Developer account

Open the RsyncUI project by Xcode. Choose the top level of the project, and select the tab `Signing & Capabilities`. Replace Team with your team.

#### No Apple Developer account

As above, but choose in `Signing Certificate` to `Sign to Run Locally`. 

#### To compile or run

Use Xcode for run, debug or build. You choose.