# Send Events To Creator Central 

The Package and Property View can send following events to Creator Central application:

| Event                                       | Description                                             |
|---------------------------------------------|---------------------------------------------------------|
| [setWidgetSettings](#set-widget-settings)   | Store data persistently for the widget's instance.      |
| [getWidgetSettings](#get-widget-settings)   | Request the persistent data for the widget's instance.  |
| [setPackageSettings](#set-package-settings) | Store data persistently for the package's instance.     |
| [getPackageSettings](#get-package-settings) | Request the persistent data for the package's instance. |
| [sendLog](#send-log)                        | Request to save the debug log to logs file.             |
| [openUrl](#open-url)                        | Open a requested web page in the external browser       |

The following events are exclusive to Package:

| Event                                              | Description                                               |
|----------------------------------------------------|-----------------------------------------------------------|
| [changeTitle](#change-widget-title)                | Change widget's title of a specific state.                |
| [changeImage](#change-widget-image)                | Change widget's image displayed now.                      |
| [changeState](#change-widget-state)                | Apply the state to an instance of a widget.               |
| [changeFontAttribute](#change-widget-title-style)  | Change widget's fonts and attributes.                     |
| [changeActionEffect](#change-widget-action-effect) | Change widget's action effect.                            |
| [getWidgetTitle](#get-widget-title)                | Request the title list for the widget's instance.         |
| [getWidgetIcon](#get-widget-icon)                  | Request the icon list for the widget's instance.          |
| [getFontAttribute](#get-widget-title-style)        | Request the font attribute of a widget.                   |
| [sendToPropertyView](#send-to-property-view)       | Send a payload to the property view                       |

The following events are exclusive to Property View:

| Event                             | Description                    |
|-----------------------------------|--------------------------------|
| [sendToPackage](#send-to-package) | Send a payload to the package. |


## Events available for Package and Property View

### Set Widget Settings

The package and property view can save data persistently for the widget's instance using the `setWidgetSettings` event. 
Note that the property view will automatically receive a [didReceiveWidgetSettings](EventsReceived.md#on-widget-settings-arrived) event with the new settings. 
Similarly, the package will automatically receive a [didReceiveWidgetSettings](EventsReceived.md#on-widget-settings-arrived) event with the new settings when the property view sends this event.

``` json
{
    "event": "setWidgetSettings",
    "context": "<uniqueIdentifier>",
    "payload": { }
}
```

| Members | Description                                                          |
|---------|----------------------------------------------------------------------|
| event   | setWidgetSettings                                                    |
| context | A unique identifier of the widget's instance.                        |
| payload | A JSON object which is persistently saved for the widget's instance. |


### Get Widget Settings

The package and property view can request the persistent data stored for the widget's instance using the `getWidgetSettings` event.

``` json
{
    "event": "getWidgetSettings",
    "context": "<uniqueIdentifier>"
}
```
| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | getWidgetSettings                             |
| context | A unique identifier of the widget's instance. |

The package and property view will receive a [didReceiveWidgetSettings](EventsReceived.md#on-widget-settings-arrived) event containing the settings for this widget:

### Set Package Settings

The package and property view can use this event to save tokens that should be available to every widget in the package.

``` json
{
    "event": "setPackageSettings",
    "context": "<uniqueIdentifier>",
    "payload": {
        "settings": { }
    }
}
```

| Members | Description                                                                             |
|---------|-----------------------------------------------------------------------------------------|
| event   | setPackageSettings                                                                      |
| context | The package's UUID in PackageConfig.json.                                               |
| payload | A JSON object which is persistently saved and available to every widget in the package. |

Please keep in your mind: when the package uses this API, the Property View will automatically receive a [didReceivePackageSettings](EventsReceived.md#on-package-settings-arrived) callback with the new settings. 
Similarly, when the Property View uses this API, the package will also receive a [didReceivePackageSettings](EventsReceived.md#on-package-settings-arrived) callback with the new settings.


### Get Package Settings

The package and Property View can request the persistent data which available to every widget in the package using the `getPackageSettings` event:

``` json
{
    "event": "getPackageSettings",
    "context": "<uniqueIdentifier>"
}
```

| Members | Description                               |
|---------|-------------------------------------------|
| event   | getPackageSettings                        |
| context | The package's UUID in PackageConfig.json. |

The package or Property View will receive an event [didReceivePackageSettings](EventsReceived.md#on-package-settings-arrived) containing the global settings:


### Send Log

The package and Property View can use the `sendLog` event to write a debug message to the logs file:

``` json
{
    "event": "sendLog",
    "payload": {
        "message": "Something need to be saved."
    }
}
```

| Members | Description   |
|---------|---------------|
| event   | sendLog       |
| payload | A JSON object |

The payload object contains the following members:

| Payload | Description                          |
|---------|--------------------------------------|
| message | A string to write to the logs file.  |


### Open Url

The package and Property View can use the `openUrl` event to open a webpage in the external browser:

``` json
{
    "event": "openUrl",
    "payload": {
        "url": "https://www.avermedia.com"
    }
}
```

| Members | Description   |
|---------|---------------|
| event   | openUrl       |
| payload | A JSON object |

The payload object contains the following members:

| Payload | Description               |
|---------|---------------------------|
| url     | A url to external website |


## Package Only Events

### Change Widget Title

The package can send a `changeTitle` event to the Creator Central application to change the title displayed on the display view of widget for a specific state.

``` json 
{
    "event": "changeTitle", 
    "context": "<uniqueIdentifier>",
    "payload": {
        "title": "New Title",
        "state": 0
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | changeTitle                                   |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Payload | Description                                                                         |
|---------|-------------------------------------------------------------------------------------|
| state   | A zero-based integer value representing the state of a widget with multiple states. |
| title   | The title to display.                                                               |


### Change Widget Image

The package can send a `changeImage` event to the Creator Central application to change the image displayed on the display view of widget.

``` json 
{
    "event": "changeImage", 
    "context": "<uniqueIdentifier>",
    "payload": {
        "image": "<base64 encoded image>"
    }
};
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | changeImage                                   |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Payload   | Description                                                                             |
|-----------|-----------------------------------------------------------------------------------------|
| image     | The image to display encoded in base64 with the image format declared in the mime type. |


### Change Widget State

The package can change the state of a widget that supports multiple states. These states are defined in [PackageConfig.json](PackageConfiguration.md)

``` json
{
    "event": "changeState",
    "context": "<uniqueIdentifier>",
    "payload": {
        "state": 0
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | changeState                                   |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Payload | Description                                                                         |
|---------|-------------------------------------------------------------------------------------|
| state   | A zero-based integer value representing the state of a widget with multiple states. |


### Change Widget Title Style

The package can send a `changeFontAttribute` event to the Creator Central application to change the font attributes of widget.

``` json 
{
    "event": "changeFontAttribute", 
    "context": "<uniqueIdentifier>",
    "payload": {
        "family": "Arial", 
        "size": 18,
        "color": "#ff8000", 
        "hAlignment": "left",
        "bold": true, 
        "italic": true, 
        "underLine": true
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | changeFontAttribute                           |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Payload    | Option   | Description                                                                             |
|------------|----------|-----------------------------------------------------------------------------------------|
| family     | Required | The font family for the widget title.                                                   |
| size       | Required | The font size for the widget title. It is a integer value limited between 6 to 18.      |
| color      | Required | Title color.                                                                            |
| hAlignment | Required | The horizontal alignment of the widget title. Support "left", "right" and "center" now. |
| bold       | Required | Show the title with bold style.                                                         |
| italic     | Required | Show the title with italic style.                                                       |
| underLine  | Required | Show the title with underline style.                                                    |


### Change Widget Action Effect

The package can send a `changeActionEffect` event to Creator Central application to change the effect displayed on the display view of widget.

``` json
{
    "event": "changeActionEffect",
    "context": "<uniqueIdentifier>",
    "payload": {
        "type": "press|clear|invalid|inactive", 
        "image": "<base64 encoded image>"
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | changeActionEffect                            |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Payload  | Required | Description                                                                                                                                                                                            |
|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type     | Required | Only supports "press", "invalid", and "clear" now.<br/><ul><li>press: widget is pressed</li><li>invalid: widget is disabled</li><li>clear: restore original state</li><li>inactive: reserved</li></ul> |
| image    | Optional | The image to display encoded in base64 with the image format declared in the mime type.                                                                                                                |


### Get Widget Title

Request the title list of the widget's instance.

``` json
{
    "event": "getWidgetTitle",
    "context": "<uniqueIdentifier>"
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | getWidgetTitle                                |
| context | A unique identifier of the widget's instance. |

The package and Property View will receive a [didReceiveWidgetTitle](EventsReceived.md#on-widget-title-arrived) event containing the settings.


### Get Widget Icon

Request the icon list of the widget's instance.

``` json
{
    "event": "getWidgetIcon",
    "context": "<uniqueIdentifier>"
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| event   | getWidgetIcon                                 |
| context | A unique identifier of the widget's instance. |

The package and Property View will receive a [didReceiveWidgetIcon](EventsReceived.md#on-widget-icon-arrived) event containing the settings.


### Get Widget Title Style

The package can request the icon list of an instance of widget using the `getFontAttribute` event.

``` json
{
    "event": "getFontAttribute",
    "context": "<uniqueIdentifier>"
}
```

| Members | Description                              |
|---------|------------------------------------------|
| event   | getFontAttribute                         |
| context | A value to identify the widget instance. |

The package and Property View will receive a [didReceiveFontAttribute](EventsReceived.md#on-widget-title-style-arrived) event containing the settings.


### Send To Property View

The package can send a payload to the Property View using the `sendToPropertyView` event:

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPropertyView",
    "context": "<uniqueIdentifier>",
    "payload": { }
}
```

| Members | Description                              |
|---------|------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json. |
| event   | sendToPropertyView                       |
| context | A value to identify the widget instance. |
| payload | A JSON object                            |

The property view will receive a [sendToPropertyView](EventsReceived.md#on-property-message-received) event containing the payload.


## Property View Only Events
### Send To Package

The property view can send a payload to the package using the `sendToPackage` event:
``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPackage",
    "context": "<uniqueIdentifier>",
    "payload": { }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | sendToPackage                                 |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The package will receive a [sendToPackage](EventsReceived.md#on-package-message-arrived) event containing the payload.
