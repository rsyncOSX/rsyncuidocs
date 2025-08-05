+++
author = "Thomas Evensen"
title = "Tweaking data"
date = "2025-03-01"
tags = ["tweaking"]
categories = ["technical details"]
+++

RsyncUI is a tool for synchronizing data between a source and a destination. While it is a standard tool, utilizing it for specialized tasks that require specific parameters can sometimes be challenging. However, you can manually adjust the data to enable its use.

RsyncUI does not validate the parameters added to the rsync command. If there are parameters that rsync does not comprehend, the task verification will result in an error. Therefore, you can freely specify the parameters you need for rsync. You can also begin with initial values and modify them in the exported JSON file. Subsequently, import the file to verify its functionality.

The "Export & Import" option is selected from the menu bar when in the main Synchronize view form. If the modified JSON becomes malformed, the import will only generate an error.

**Important:** The blue keywords in the provided JSON sample are internal to RsyncUI and may not always align with the views displayed. For instance, the keyword "offsiteCatalog" serves as the internal storage for "destination." The variation in internal keywords is solely due to the history, preventing users from modifying or adding tasks when new versions of RsyncUI are released.

```json
[{"offsiteCatalog":"Destination Folder\/","parameter2":"--verbose","backupID":"Synchronize ID test","parameter3":"--compress","dateRun":"","parameter8":"--userparam1=value","parameter9":"--userparam2=value","parameter12":"--userparam5=value","parameter1":"--archive","task":"synchronize","offsiteUsername":"Remote User","halted":0,"parameter11":"--userparam4=value","id":"E62C46B3-5C57-4C22-864E-359F96D13C2E","parameter13":"--userparam6=value","parameter14":"--userparam7= value","hiddenID":1,"parameter10":"--userparam3=value","localCatalog":"Source Folder\/","offsiteServer":"Remote Server","parameter4":"--delete"}]
```
