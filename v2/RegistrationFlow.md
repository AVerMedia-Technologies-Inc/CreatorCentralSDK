# Registration Flow

## Package Registration

When launching the Creator Central application spawns one instance of a package. The package will be called as the following:

- For JavaScript packages, its `connectCreatorCentral()` is called with specific parameters.
- For compiled packages written for example in C++ or Objective-C, its `main()` function is called with specific parameters.

These parameters contain the port and unique identifier for the communication between your codes and the Creator Central application.

- [JavaScript Package Registration](#javascript-package-registration)
- [Compiled package Registration](#compiled-package-registration)
- [Property View Registration](#property-view-registration)

You can check our [samples](Samples.md) to find further information.

## JavaScript Package Registration

For a JavaScript package, you need to declare the following JavaScript function in your package:

``` js
function connectCreatorCentral(inPort, inPackageUUID, inRegisterEvent, inInfo)
```
| Members         | Description                                                                                              |
|-----------------|----------------------------------------------------------------------------------------------------------|
| inPort          | The port used to create the WebSocket.                                                                   |
| inPackageUUID   | The unique identifier string to register the package once the WebSocket is opened.                       |
| inRegisterEvent | A registration key string that should be used once the WebSocket is opened.                              |
| inInfo          | A JSON object containing Creator Central information. See [Creator Central Info](#creator-central-info). |

This function is called when the package is loaded and should do the following:

### Create the WebSocket to Creator Central

You should create a WebSocket with the designated port by Creator Central.

``` js
websokcet = new WebSocket("ws://localhost:" + inPort);
```

###  Register your package to Creator Central

When the WebSocket is open, the package needs to register itself to Creator Central.

``` js
websocket.onopen = function()
{
    const json = {
        "event": inRegisterEvent,
        "uuid": inPackageUUID
    };

    websocket.send(JSON.stringify(json));
}
```

### Receive and send via WebSocket

After performing these two steps, the package should receive the events through the function:

``` js
websocket.onmessage = function(evt)
```


## Compiled package Registration

If your package is a compiled package(C++, Swift, C#, ...), the command-line tool will be executed with the following parameters:

```shell
foo.exe -port port -packageUUID packageUUID -registerEvent registerEvent -info info
```

| Arguments     | Description                                                                        |
|---------------|------------------------------------------------------------------------------------|
| port          | The port used to create the WebSocket.                                             |
| packageUUID   | The unique identifier string to register the package once the WebSocket is opened. |
| registerEvent | A registration key string that should be used once the WebSocket is opened.        |
| info          | A JSON object containing Creator Central information.                              |


## Property View Registration

If a widget is configurable, you should provide an HTML page for the property view.
A property view registration is similar to [JavaScript Package Registration](#javascript-package-registration) but with extra arguments.
These parameters contain the port and unique identifier to use for communication with the Creator Central application.
Your JavaScript function would be as below:

``` js
function connectCreatorCentral(inPort, inPropertyViewUUID, inRegisterEvent, inInfo, inWidgetInfo)
```

| Members            | Description                                                                                              |
|--------------------|----------------------------------------------------------------------------------------------------------|
| inPort             | The port used to create the WebSocket.                                                                   |
| inPropertyViewUUID | The unique identifier string to register the property view once the WebSocket is opened.                 |
| inRegisterEvent    | The event type that should be used to register the property view once the WebSocket is opened.           |
| inInfo             | A JSON object containing Creator Central information. See [Creator Central Info](#creator-central-info). |
| inWidgetInfo       | A JSON object containing information about the widget. See [Widget Info](#widget-info).                  |

This function is called when property view is displayed and should:

### Create the WebSocket to Creator Central

You should create a WebSocket with the designated port by Creator Central.

``` js
websocket = new WebSocket("ws://localhost:" + inPort);
```

###  Register your package to Creator Central

When the WebSocket is open, the property view needs to register itself to Creator Central.

``` js
websokcet.onopen = function()
{
    const json = {
        "event": inRegisterEvent,
        "uuid": inPropertyViewUUID
    };

    websocket.send(JSON.stringify(json));
};
```

### Receive and send via WebSocket

After performing these two steps, the package should receive the events through the function:

``` js
websocket.onmessage = function(evt)
```

## Creator Central Info

The `info` argument used in the registration flow is a JSON object like:

<b>Currently Creator Central only provides the information of the application and the OS platform.</b>

``` json
{
    "application": {
        "language": "en",
        "platform": "mac",
        "platformVersion": "11.0",
        "version": "1.1.0.75"
    }
}
```

| Application Members | Description                                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------|
| language            | In which language used by Creator Central now. Possible values are `en`, `ja`, `zh_TW`, `de`, `ko` |
| platform            | On which platform the Creator Central is running. Possible values are `win` and `mac` .            |
| platformVersion     | The operation system version.                                                                      |
| version             | The Creator Central application version.                                                           |


## Widget Info

The `widgetInfo` parameter is a JSON object contains the following information:

``` json
{
    "widget": "com.avermedia.example.widget1",
    "context": "uniqueIdentifier",
    "payload": {
        "settings": { }
    }
}
```

| Members | Description                              |
|---------|------------------------------------------|
| widget  | The widget's category                    |
| context | A value to identify the widget instance. |
| payload | A JSON object                            |

The payload contains:

| Payload   | Description                                                           |
|-----------|-----------------------------------------------------------------------|
| settings  | This JSON contains data that you can set and are stored persistently. |
