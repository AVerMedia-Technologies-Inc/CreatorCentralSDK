# Creator Central Package SDK Version 2 (Beta)
![Creator Central SDK](https://img.shields.io/badge/SDK-2.0.5-yellow)
![Creator Central](https://img.shields.io/badge/Creator%20Central-1.1.2.29-orange)
![Creator Central Simulator](https://img.shields.io/badge/Simulator-1.0.0.6-blue)

**Welcome to Creator Central SDK Version 2 documentation.**

We will describe how you can create widgets to enhance of the ability of AVerMedia Creator Central application.

```
Note: SDK V2 is under heavy development, so the APIs are still subject to change.

Please come back and check our documents when possible.
```

## Overview
- You can read [Terminology](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Terminology) about the Creator Central application.
- In [Architecture](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Architecture) section, we will discuss how will Creator Central work with your widgets.
- Creator Central will use [PackageConfig.json](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Package-Configuration) to identify all widgets and packages.
- Read [Registration Flow](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Registration-Flow) to understand how to start interaction with Creator Central.
- Understand how your widget is displayed in [Display View](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Display-View)
- You can [send events](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central) to Creator Central and [receive events](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Receive-Events-from-Creator-Central) from Creator Central.
- Manage your widget configuration in [Property View](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Property-View)
- We have some [sample widgets](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Samples) that can help you start your custom widgets.
- Get your [AX devices with Creator Central](https://www.avermedia.com/gaming/creatorcentral) or try our simulator in [Releases](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/releases).

## What's New

### New Event from Creator Central

A new [applicationWillTerminate](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Receive-Events-from-Creator-Central#get-package-settings) event to notify all packages that app will terminate after 3 seconds.
When uninstalling a package from Creator Central, the package will also receive this message.

### Multi-Action Support SDK Widgets

Your widgets can now be added to Multi-Action list.
A new field `MultiActionSupported` is added to identify if your widget can be added. By default, it will be true.

Check [PackageConfig.json](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Package-Configuration) for more information.

### Localization of PackageConfig.json

You can now provide the localizations for PackageConfig.json. Check [Localization](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Package-Configuration#localization) section in [PackageConfig.json](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Package-Configuration).

### Bug fixes

- Add `layout` field in [widgetWillDisappear](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Receive-Events-from-Creator-Central#widget-disappear)
- Add retry loop to launch newly installed package.
- Fix package process did not be terminated after uninstallation.
- Fix switching to invalid widget state will crash the app.
- Remove duplicated `didReceiveWidgetSettings` event when sending `propertyViewDidAppear` event.
- Increase `changeIcon` and `changeImage` refresh rate to 16fps. (to match device limitation)
- Simulator updated to v1.0.0.6 for SDK v2.0.5 with handful fixes
- Add stdout/stderr output window for binary apps in Simulator.

## Downloads
### Creator Central App Installer
- Windows [AVerMedia_Creator_Central_Installer_v1.1.2.29.exe](https://s3.us-west-2.amazonaws.com/storage.avermedia.com/web_release_www/AVerMedia_Creator_Central_Installer_v1.1.2.29_23011015.exe)
- macOS [AVerMedia+Creator+Central_V1.1.2.29.pkg](https://s3.us-west-2.amazonaws.com/storage.avermedia.com/web_release_www/software/AVerMedia+Creator+Central_V1.1.2.29.pkg)
### Creator Central Simulator
- Windows [Creator.Central.Simulator_v1.0.0.6.zip](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/releases/download/SDK_v2.0.5/Creator.Central.Simulator_v1.0.0.6.zip)
- macOS [CreatorCentralSimulator_v1.0.0.6.dmg.zip](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/releases/download/SDK_v2.0.5/CreatorCentralSimulator_v1.0.0.6.dmg.zip)

