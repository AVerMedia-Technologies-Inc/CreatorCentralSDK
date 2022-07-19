Event Received
===

When Creator Central load the Package, it will send events to them.
Both the Package and the Property View can receive these events:


| Event | Description |
| -------- | -------- |
| didReceiveWidgetSettings | Event received after sending the getWidgetSettings event to retrieve the persistent data stored for the widget. |
| didReceivePackageSettings | Event received after sending the getPackageSettings event to retrieve the persistent data stored for the Package. |

These events will be sent to Package. The Property View won't receive them.

| Event | Description |
| -------- | -------- |
| actionDown | When the user presses a display view on the panel or a function key of AX devices, the package will receive the actionDown event. |
| actionUp | When the user releases his finger from the panel or a function key of AX devices, the package will receive the actionUp event. |
| actionTriggered | When the user presses a display view and then releases within it, the package will receive the actionTriggered event. |
| widgetWillAppear | When an instance of a widget is displayed on Creator Central, for example, when the profile loaded, the package will receive a willAppear event. |
| widgetWillDisappear | When switching profile, an instance of a widget will be invisible, the package will receive a willDisappear event. |
| propertyViewDidAppear | When user selected a widget on the panel, the package will receive this event. |
| propertyViewDidDisappear | When user selected a different widget on the panel, the package will receive this event.  |
| sendToPackage | When user selected a different widget on the panel, the package will receive this event.  |
| didReceiveWidgetTitle | Event received after sending the getWidgetTitle event or user change the title manually. | 
| didReceiveWidgetIcon | Event received after sending the getWidgetIcon event or user select an icon from icon builder or local disk manually. |
| didReceiveFontAttribute | Event received after sending the getFontAttribute event or user change the font attribute manually. |

The Property View will receive these events.

| Event | Description |
| -------- | -------- |
| sendToPropertyView | When Package calls setToPropertyView |

## didReceiveWidgetSettings

``` json
var json = {
    "widget": "com.avermedia.example.widget1", 
    "event": "didReceiveWidgetSettings", 
    "context": <uniqueIdentifier>, 
    "payload": {<json data>}
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | didReceiveWidgetSettings |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json data contains persistently stored data. |

## didReceivePackageSettings

``` json
var json = {
    "event": "didReceivePackageSettings", 
    "payload": {<json data>}
};
```

| Members | Description |
| -------- | -------- |
| event | didReceivePackageSettings |
| payload | A json data contains persistently stored data. | 

## actionDown

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "actionDown", 
    "context": <uniqueIdentifier>,
    "payload": {
        "state": 0
    }
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | actionDown |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json object |


The payload object contains the following members:


| Members | Description |
| -------- | -------- |
| state | Only set when the widget has multiple states. The 0-based value contains the current state of the action. |

## actionUp

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "actionUp", 
    "context": <uniqueIdentifier>,
    "payload": {
        "state": 0
    }
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | actionUp |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json object |

The payload object contains the following members:

| Members | Description |
| -------- | -------- |
| state | Only set when the widget has multiple states. The 0-based value contains the current state of the action. |

## actionTriggered

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "actionTriggered", 
    "context": <uniqueIdentifier>,
    "payload": {
        "state": 0
    }
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | actionTriggered |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json object |

The payload object contains the following members:

| Members | Description |
| -------- | -------- |
| state | Only set when the widget has multiple states. The 0-based value contains the current state of the action. |


## widgetWillAppear

The package will receive this event when:
- the user switches profiles.
- the user drag a widget from Widget List to Panel.

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "widgetWillAppear", 
    "context": <uniqueIdentifier>,
    "payload": {
        "state": 0
    }
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | widgetWillAppear |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json object |

The payload object contains the following members:

| Members | Description |
| -------- | -------- |
| state | Only set when the widget has multiple states. The 0-based value contains the current state of the action. |

## widgetWillDisappear
The package will receive this event when:
- the user switches profiles.
- the user deletes a widget.

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "widgetWillDisappear", 
    "context": <uniqueIdentifier>,
    "payload": {
        "state": 0
    }
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | widgetWillDisappear |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json object |

The payload object contains the following members:

| Members | Description |
| -------- | -------- |
| state | Only set when the widget has multiple states. The 0-based value contains the current state of the action. |

## propertyViewDidAppear

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "propertyViewDidAppear", 
    "context": <uniqueIdentifier>
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | propertyViewDidAppear |
| context | The unique identifier used to identify the instance's widget. |


## propertyViewDidDisappear

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "propertyViewDidDisappear", 
    "context": <uniqueIdentifier>
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | propertyViewDidDisappear |
| context | The unique identifier used to identify the instance's widget. |

## sendToPackage
The package will receive a ```sendToPackage``` event when the property view sends a ```sendToPackage``` event:

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPackage", 
    "context": <uniqueIdentifier>,
    "payload": {<json data>}
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | sendToPackage |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json data |

When the package received this event, it will change the properties or data of a specific widget based on the JSON object.

## didReceiveWidgetTitle

``` json
var json = {
    "event": "didReceiveWidgetTitle", 
    "payload": [<array of widget title>]
};
```

| Members | Description |
| -------- | -------- |
| event | didReceiveWidgetTitle |
| payload | A json data contains the array of widget title. | 

## didReceiveWidgetIcon

``` json
var json = {
    "event": "didReceiveWidgetIcon", 
    "payload": [<array of widget icon>]
};
```

| Members | Description |
| -------- | -------- |
| event | didReceiveWidgetIcon |
| payload | A json data contains the array of widget icon. | 

## didReceiveFontAttribute

``` json
var json = {
    "event": "didReceiveFontAttribute", 
    "payload": {
    		"family": "Arial",
    		"size": 13,
    		"color": "#ff8000",
    		"hAlignment": "center",
    		"bold": false,
    		"italic": false,
    		"underLine": false
    	}
};
```

| Members | Description |
| -------- | -------- |
| event | didReceiveFontAttribute |
| payload | A json data contains the attributes of widget. | 

## sendToPropertyView
The property view will receive a **sendToPropertyView** event when the package sends a **sendToPropertyView** event:

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPropertyView", 
    "context": <uniqueIdentifier>,
    "payload": {<json data>}
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget's category. |
| event | sendToPropertyView |
| context | The unique identifier used to identify the instance's widget. |
| payload | A json data |
