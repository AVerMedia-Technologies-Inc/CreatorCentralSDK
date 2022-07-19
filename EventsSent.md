Events Sent
===

The package and Property View can send following events to Creator Central application:

| Event | Description |
| -------- | -------- |
| setWidgetSettings | Store data persistently for the widget's instance. |
| getWidgetSettings | Request the persistent data for the widget's instance. |
| setPackageSettings | Store data persistently for the package's instance. |
| getPackageSettings | Request the persistent data for the package's instance. |
| sendLog | Request to save the debug log to logs file. |

The following events is additional to package:

| Event | Description |
| -------- | -------- |
| changeTitle | Change the title of an instance of a widget. |
| changeImage | Change the image displayed by an instance of a widget. |
| changeState | Apply the state to an instance of a widget. |
| changeFontAttribute | Change the font attribute of an instance of widget. |
| changeActionEffect | Apply the effect to an instance of a widget. |
| getWidgetTitle | Request the title list of a widget. |
| getWidgetIcon | Request the icon list of a widget. |
| getFontAttribute | Request the font attribute of a widget. |
| sendToPropertyView | Send a payload to the property view |

The following events is additional to property view:

| Event | Description |
| -------- | -------- |
| sendToPackage | Send a payload to the package. |

## setWidgetSettings

The package and property view can save data persistently for the widget's instance using the setWidgetSettings event. Note that the property view will automatically receive a [```didReceiveWidgetSettings```](/EventsReceived.md#didReceiveWidgetSettings) event with the new settings. Similarly, the package will automatically receive a ```didReceiveWidgetSettings``` event with the new settings when the property view sends this event.

``` json
var json = {
    "event": "setWidgetSettings",
    "context": uniqueValue,
    "payload": {<json data>}
};
```

| Members | Description |
| -------- | -------- |
| event | setWidgetSettings. |
| context | A value to identify the instance's widget or Property View. This value is received by the Property View as a parameter of the connectCreatorCentral function. |
| payload | A JSON object which is persistently saved for the widget's instance. |

## getWidgetSettings

The package and property view can request the persistent data stored for the widget's instance using the ```getWidgetSettings``` event.

``` json
var json = {
    "event": "getWidgetSettings",
    "context": uniqueIdentifier
};
```

| Members | Description |
| -------- | -------- |
| event | getWidgetSettings. |
| context | A value to identify the instance's widget or Property View. This value is received by the Property View as a parameter of the connectCreatorCentral function. |

The package or property view will receive an event ```didReceiveWidgetSettings``` containing the settings for this widget:
``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "didReceiveWidgetSettings",
    "context": uniqueIdentifier,
    "payload": {
        "settings": {<json data>}
    }
};
```


## setPackageSettings

The package and property view can use this event to save tokens that should be available to every widget in the package.

``` json
var json = {
    "event": "setPackageSettings",
    "context": uniqueIdentifier,
    "payload": {
        "settings": {<json data>}
    }
};
```

| Members | Description |
| -------- | -------- |
| event | setPackageSettings. |
| context | A value to identify the package or Property View. This value is received by the Property View as a parameter of the connectCreatorCentral function. |
| payload | A json object which is persistently saved and available to every widget in the package. |

Please keep in your mind: when the package uses this API, the Property View will automatically receive a ```didReceivePackageSettings``` callback with the new settings. Similarly, when the Property View uses this API, the package will automatically receive a ```didReceivePackageSettings``` callback with the new settings.

## getPackageSettings

The package and Property View can request the persistent data which available to every widget in the package using the **getPackageSettings** event:

``` json
var json = {
    "event": "getPackageSettings",
    "context": uniqueIdentifier
};
```

| Members | Description |
| -------- | -------- |
| event | getPackageSettings |
| context | A value to identify the package or Property View. This value is received by the Property View as a parameter of the connectCreatorCentral function. |

The package or Property View will receive an event ```didReceivePackageSettings``` containing the global settings:

``` json
var json = {
    "event": "didReceivePackageSettings",
    "payload": {
        settings: {<json data>}
    }
}
```

## sendLog

The package and Property View can use the **sendLog** event to write a debug message to the logs file:
``` json
var json = {
    "event": "sendLog",
    "payload": {
        "message": "Something need to be saved."
    }
};
```

| Members | Description |
| -------- | -------- |
| event | sendLog |
| payload | A json object |

The payload object contains the following members:

| Payload | Description |
| -------- | -------- |
| message | A string to write to the logs file. |

## changeTitle

The package can send a **changeTitle** event to the Creator Central application to change the title displayed on the display view of widget.

``` json 
var json = {
    "event": "changeTitle", 
    "context": uniqueIdentifier,
    "payload": {
        "title": "New Title",
        "state": zero-based integer
    }
};
```

| Members | Description |
| -------- | -------- |
| event | changeTitle |
| context | A value to identify the widget instance you want to modify |
| payload | A json object |

The payload object contains the following members:

| Payload | Description |
| -------- | -------- |
| title | The title to display. |
| state | A 0-based integer value representing the state of a widget with multiple states. |

## changeImage

The package can send a **changeImage** event to the Creator Central application to change the image displayed on the display view of widget.

``` json 
var json = {
    "event": "changeImage", 
    "context": uniqueIdentifier,
    "payload": {
        "image": <base64 encoded image>,
        "state": zero-based integer
    }
};
```

| Members | Description |
| -------- | -------- |
| event | changeImage |
| context | A value to identify the widget instance you want to modify |
| payload | A json object |

The payload object contains the following members:

| Payload | Description |
| -------- | -------- |
| image | The image to display encoded in base64 with the image format declared in the mime type. |
| state | A 0-based integer value representing the state of a widget with multiple states. |

## changeState

The package can change the state of a widget supporting multiple states:
``` json
var json = {
    "event": "changeState",
    "context": uniqueIdentifier,
    "payload": {
        "state": zero-based integer
    }
};
```

| Members | Description |
| -------- | -------- |
| event | changeState |
| context | A value to identify the widget instance you want to modify. |
| payload | A json object |

The payload object contains the following members:

| Payload | Description |
| -------- | -------- |
| state | A 0-based integer value representing the state of a widget with multiple states. |

## changeFontAttribute
The package can send a **changeFontAttribute** event to the Creator Central application to change the font attributes of widget.

``` json
var json = {
	"event": "changeFontAttribute",
	"context": uniqueIdentifier,
	"payload": {
		"family": "Arial",
		"size": 18, # support 6 ~ 18
		"color": "#ff8000",
		"hAlignment": "left",
		"bold": false,
		"italic": false,
		"underLine": false
	}
};
```

| Members | Description |
| -------- | -------- |
| event | changeFontAttribute |
| context | A value to identify the widget instance you want to modify. |
| payload | A json object |

The payload object contains the following members:

| Payload | Description |
| -------- | -------- |
| family | The font family for the widget title. |
| size | The font size for the widget title. |
| color | Title color. |
| hAlignment | The horizontal alignment of the widget title. Support "left", "right" and "center" now. |
| bold | Show the title with bold style. |
| italic | Show the title with italic style. |
| underLine | Show the title with underline style. |

## changeActionEffect
The package can send a **changeActionEffect** event to Creator Central application to change the effect displayed on the display view of widget.

``` json
var json = {
	"event": "changeActionEffect",
	"context": uniqueIdentifier,
	"payload": {
		"type": "press",
		"image": <base64 encoded image>
	}
};
```

| Members | Description |
| -------- | -------- |
| event | changeActionEffect |
| context | A value to identify the widget instance you want to modify. |
| payload | A json object |

The payload object contains the following members:

| Payload | Description |
| -------- | -------- |
| type | The type of effect. Support "press", "clear", "invalid" and "inactive" now. |
| image | The image to display encoded in base64 with the image format declared in the mime type. |

## getWidgetTitle
The package can request the title list of an instance of widget using the **getWidgetTitle** event.

``` json
var json = {
	"event": "getWidgetTitle",
	"context": uniqueIdentifier
};
``` 

| Members | Description |
| -------- | -------- |
| event | getWidgetTitle |
| context | A value to identify the widget instance you want to modify. |

## getWidgetIcon

The package can request the icon list of an instance of widget using the **getWidgetIcon** event.

``` json
var json = {
	"event": "getWidgetIcon",
	"context": uniqueIdentifier
};
``` 

| Members | Description |
| -------- | -------- |
| event | getWidgetIcon |
| context | A value to identify the widget instance. |

## getFontAttribute

The package can request the icon list of an instance of widget using the **getFontAttribute** event.

``` json
var json = {
	"event": "getFontAttribute",
	"context": uniqueIdentifier
};
``` 

| Members | Description |
| -------- | -------- |
| event | getFontAttribute |
| context | A value to identify the widget instance. |

## sendToPackage

The property view can send a payload to the package using the ```sendToPackage``` event:
``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPackage",
    "context": uniqueIdentifier,
    "payload": {<json data>}
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget category |
| event | sendToPackage |
| context | A value to identify the widget instance. |
| payload | A json object |

The package will receive event ```sendToPackage``` containing the payload:

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPackage",
    "context": uniqueIdentifier,
    "payload": {<json data>}
};
```

## sendToPropertyView

The package can send a payload to the Property View using the ```sendToPropertyView``` event:

``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPropertyView",
    "context": uniqueIdentifier,
    "payload": {<json data>}
};
```

| Members | Description |
| -------- | -------- |
| widget | The widget category |
| event | sendToPropertyView |
| context | A value to identify the widget instance. |
| payload | A json object |

The property view will receive event ```sendToPropertyView``` containing the payload:
``` json
var json = {
    "widget": "com.avermedia.example.widget1",
    "event": "sendToPropertyView",
    "context": uniqueIdentifier,
    "payload": {<json data>}
};
```
