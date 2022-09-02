# Send Events To Creator Central 

The Package and Property View can send following events to Creator Central application:

| Event                                                                                                                                          | Description                                               |
|------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| [setWidgetSettings](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#set-widget-settings)   | Store data persistently for the widget's instance.        |
| [getWidgetSettings](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#get-widget-settings)   | Request the persistent data for the widget's instance.    |
| [setPackageSettings](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#set-package-settings) | Store data persistently for the package's instance.       |
| [getPackageSettings](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#get-package-settings) | Request the persistent data for the package's instance.   |
| [sendLog](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#send-log)                        | Request to save the debug log to logs file.               |
| [openUrl](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#open-url)                        | Open a requested web page in the external browser         |

The following events are exclusive to Package:

| Event                                                                                                                                                 | Description                                               |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| [changeTitle](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#change-widget-title)                | Change widget's title of a specific state.                |
| [changeImage](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#change-widget-image)                | Change widget's image displayed now.                      |
| [changeState](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#change-widget-state)                | Apply the state to an instance of a widget.               |
| [changeFontAttribute](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#change-widget-title-style)  | Change widget's fonts and attributes.                     |
| [changeActionEffect](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#change-widget-action-effect) | Change widget's action effect.                            |
| [getWidgetTitle](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#get-widget-title)                | Request the title list for the widget's instance.         |
| [getWidgetIcon](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#get-widget-icon)                  | Request the icon list for the widget's instance.          |
| [getFontAttribute](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#get-widget-title-style)        | Request the font attribute of a widget.                   |
| [sendToPropertyView](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#send-to-property-view)       | Send a payload to the property view                       |

The following events are exclusive to Property View:

| Event                                                                                                                                | Description                    |
|--------------------------------------------------------------------------------------------------------------------------------------|--------------------------------|
| [sendToPackage](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central#send-to-package) | Send a payload to the package. |

Check [Send Events To Creator Central](https://github.com/AVerMedia-Technologies-Inc/CreatorCentralSDK/wiki/Send-Events-To-Creator-Central) page for latest update.
