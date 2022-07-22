# Receive Events from Creator Central

When Creator Central loads the Package, it will send events to them.
Both the Package and the Property View can receive these events:

| Event                                                     | Description                                                                    |
|-----------------------------------------------------------|--------------------------------------------------------------------------------|
| [didReceiveWidgetSettings](#on-widget-settings-arrived)   | When a widget is displayed or a widget setting is changed.                     |
| [didReceivePackageSettings](#on-package-settings-arrived) | When a [getPackageSettings](EventsSent.md#get-package-settings) event is sent. |

These events will be sent to Package only. 

| Event                                                     | Description                                                                                            |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| [actionDown](#action-down)                                | When a user pressed the widget on the panel or a function key of AX devices.                           |
| [actionUp](#action-up)                                    | When a user released his finger from the panel or a function key of AX devices.                        |
| [actionTriggered](#action-triggered)                      | When a user pressed a widget and then released within it.                                              |
| [widgetWillAppear](#widget-appear)                        | When an instance of a widget is displayed on Creator Central.                                          |
| [widgetWillDisappear](#widget-disappear)                  | When switching profile, an instance of a widget will be invisible.                                     |
| [propertyViewDidAppear](#property-view-appear)            | When the Property View is displayed in the Panel.                                                      |
| [propertyViewDidDisappear](#property-view-disappear)      | When the Property View is removed from the Panel.                                                      |
| [sendToPackage](#on-package-message-arrived)              | When a message is sent via [sendToPackage](EventsSent.md#send-to-package).                             |
| [didReceiveWidgetTitle](#on-widget-title-arrived)         | When [getWidgetTitle](EventsSent.md#get-widget-title) event is sent or a user changes the title.       | 
| [didReceiveWidgetIcon](#on-widget-icon-arrived)           | When [getWidgetIcon](EventsSent.md#get-widget-icon) event is sent or a user changes an icon.           |
| [didReceiveFontAttribute](#on-widget-title-style-arrived) | When [getFontAttribute](EventsSent.md#get-widget-title-style) event is sent or user changes the style. |

The Property View will receive these events. The Package won't receive them.

| Event                                               | Description                                                                          |
|-----------------------------------------------------|--------------------------------------------------------------------------------------|
| [sendToPropertyView](#on-property-message-received) | When a message is sent via [setToPropertyView](EventsSent.md#send-to-property-view). |


## Events can be received in Package and Property View

### On Widget Settings Arrived

This event will be sent to Package and Property View under the following scenario.
- A [getWidgetSettings](EventsSent.md#get-widget-settings) event is sent to retrieve the persistent data stored for the widget.
- A Widget is loaded to be displayed in the Panel.
- A [setWidgetSettings](EventsSent.md#set-widget-settings) event is sent to store a persistent copy for the widget.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "didReceiveWidgetSettings",
    "context": "<uniqueIdentifier>",
    "payload": { }
}
```

| Members | Description                                    |
|---------|------------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.       |
| event   | didReceiveWidgetSettings                       |
| context | A unique identifier of the widget's instance.  |
| payload | A JSON data contains persistently stored data. |


### On Package Settings Arrived

A `didReceivePackageSettings` event will be received after sending the [getPackageSettings](EventsSent.md#get-package-settings) event to retrieve the persistent data stored for the Package.

``` json
{
    "event": "didReceivePackageSettings",
    "payload": { }
}
```

| Members | Description                                    |
|---------|------------------------------------------------|
| event   | didReceivePackageSettings                      |
| payload | A JSON data contains persistently stored data. | 


## Events can be received in Package only

### Action Down

When the user presses a display view on the panel or a function key of AX devices, the package will receive the `actionDown` event.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "actionDown",
    "context": "<uniqueIdentifier>",
    "payload": {
        "state": 0
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | actionDown                                    |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Members | Description                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| state   | Only set when the widget has multiple states. The zero-based value contains the current state of the action. |


### Action Up

When the user releases his finger from the panel or a function key of AX devices, the package will receive the `actionUp` event.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "actionUp",
    "context": "<uniqueIdentifier>",
    "payload": {
        "state": 0
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | actionUp                                      |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Members   | Description                                                                                                  |
|-----------|--------------------------------------------------------------------------------------------------------------|
| state     | Only set when the widget has multiple states. The zero-based value contains the current state of the action. |


### Action Triggered

When the user presses a display view and then releases within it, the package will receive the `actionTriggered` event.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "actionTriggered",
    "context": "<uniqueIdentifier>",
    "payload": {
        "state": 0
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | actionTriggered                               |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Members  | Description                                                                                                  |
|----------|--------------------------------------------------------------------------------------------------------------|
| state    | Only set when the widget has multiple states. The zero-based value contains the current state of the action. |


### Widget Appear

The package will receive `willAppear` event when:
- A user switches profiles.
- A user drags a widget from Widget List to Panel.
- Creator Central is started

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "widgetWillAppear",
    "context": "<uniqueIdentifier>",
    "payload": {
        "state": 0
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | widgetWillAppear                              |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Members  | Description                                                                                                  |
|----------|--------------------------------------------------------------------------------------------------------------|
| state    | Only set when the widget has multiple states. The zero-based value contains the current state of the action. |


### Widget Disappear

The package will receive `willDisappear` event when:
- A user switches profiles.
- A user deletes a widget.
- An instance of a widget becomes invisible

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "widgetWillDisappear",
    "context": "<uniqueIdentifier>",
    "payload": {
        "state": 0
    }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | widgetWillDisappear                           |
| context | A unique identifier of the widget's instance. |
| payload | A JSON object                                 |

The payload object contains the following members:

| Members | Description                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| state   | Only set when the widget has multiple states. The zero-based value contains the current state of the action. |


### Property View Appear

The package will receive `propertyViewDidAppear` event when the Property View is displayed in the Panel.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "propertyViewDidAppear",
    "context": "<uniqueIdentifier>"
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | propertyViewDidAppear                         |
| context | A unique identifier of the widget's instance. |


### Property View Disappear

The package will receive `propertyViewDidDisappear` event when the Property View is removed from the Panel.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "propertyViewDidDisappear",
    "context": "<uniqueIdentifier>"
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | propertyViewDidDisappear                      |
| context | A unique identifier of the widget's instance. |


### On Package Message Arrived

The package will receive a `sendToPackage` event when the property view sends a [sendToPackage](EventsSent.md#send-to-package) event:

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
| payload | A JSON data                                   |

When the package received this event, it will change the properties or data of a specific widget based on the JSON object.


### On Widget Title Arrived

The package will receive `didReceiveWidgetTitle` event when:
- A [getWidgetTitle](EventsSent.md#get-widget-title) event is sent.
- A user changes the title of the widget.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "didReceiveWidgetTitle",
    "context": "<uniqueIdentifier>",
    "payload": [ ]
}
```

| Members | Description                                     |
|---------|-------------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.        |
| event   | didReceiveWidgetTitle                           |
| context | A unique identifier of the widget's instance.   |
| payload | A JSON data contains the array of widget title. | 


### On Widget Icon Arrived

The package will receive `didReceiveWidgetIcon` event when:
- A [getWidgetIcon](EventsSent.md#get-widget-icon) event is sent.
- A user changes the icon of the widget.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "didReceiveWidgetIcon",
    "context": "<uniqueIdentifier>",
    "payload": [ ]
}
```

| Members | Description                                    |
|---------|------------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.       |
| event   | didReceiveWidgetIcon                           |
| context | A unique identifier of the widget's instance.  |
| payload | A JSON data contains the array of widget icon. | 

### On Widget Title Style Arrived

The package will receive `didReceiveFontAttribute` event when:
- A [getFontAttribute](EventsSent.md#get-widget-title-style) event is sent.
- A user changes the font attribute manually.

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "didReceiveFontAttribute",
    "context": "<uniqueIdentifier>",
    "payload": {
        "family": "Arial",
        "size": 13,
        "color": "#ff8000",
        "hAlignment": "center",
        "bold": false,
        "italic": false,
        "underLine": false
    }
}
```

| Members | Description                                    |
|---------|------------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.       |
| event   | didReceiveFontAttribute                        |
| context | A unique identifier of the widget's instance.  |
| payload | A JSON data contains the attributes of widget. | 


## Events can be received in Package and Property View

### On Property Message Received

The property view will receive a `sendToPropertyView` event when the package sends a [sendToPropertyView](EventsSent.md#send-to-property-view) event:

``` json
{
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPropertyView",
    "context": "<uniqueIdentifier>",
    "payload": { }
}
```

| Members | Description                                   |
|---------|-----------------------------------------------|
| widget  | The widget's UUID in PackageConfig.json.      |
| event   | sendToPropertyView                            |
| context | A unique identifier of the widget's instance. |
| payload | A JSON data                                   |
