# Package Configuration

## PackageConfig.json Example

Here is an example of [PackageConfig.json](https://github.com/AVerMedia-Technologies-Inc/NumberToolbox/blob/main/Source/PackageConfig.json) file from our [NumberToolbox](https://github.com/AVerMedia-Technologies-Inc/NumberToolbox) sample.
Developers should modify the fields for your Package/Widget.

``` json 
{
    "Author": "Mike Yeh",
    "Description": "This kit contains counter and random number generator toolbox",
    "Name": "Number Toolbox",
    "UUID": "com.avermedia.package.number.toolbox",
    "Icon": "images/mainpage_btn_tool_counter.svg",
    "URL": "https://www.avermedia.com/gaming/creatorcentral",
    "Version": "1.0.0",
    "Runtime": {
        "mac": {
            "type": "bin",
            "target": "Template.app",
            "MinimumVersion": "11.0"
        },
        "win": {
            "type": "bin",
            "target": "Template.exe",
            "MinimumVersion": "10.0"
        }
    },
    "CreatorCentral": {
        "MinimumVersion": "1.1",
        "SDKVersion": 2
    },
    "Widgets": [
        {
            "Name": "Counter",
            "Icon": "images/mainpage_btn_tool_counter.svg",
            "Tooltip": "Counter",
            "UUID": "com.avermedia.widget.counter",
            "PropertyViewPath": "property/counter/index.html",
            "States": [
                {
                    "Image": "images/mainpage_btn_tool_counter.svg",
                    "Title": "Counter"
                }
            ],
            "Layouts": [
                {
                    "Title": "Counter",
                    "Icon": "images/mainpage_btn_tool_counter.svg",
                    "Width": 1,
                    "Height": 1
                }
            ]
        },
        {
            "Name": "Random",
            "Icon": "images/mainpage_btn_tool_random_number.svg",
            "Tooltip": "Random",
            "UUID": "com.avermedia.widget.random.generator",
            "PropertyViewPath": "property/random/index.html",
            "States": [
                {
                    "Image": "images/mainpage_btn_tool_random_number_bg.svg",
                    "Title": "Random"
                }
            ],
            "TitleEditable": true,
            "TitleViewEditable": true,
            "IconEditable": true
        }
    ]
}
```


## Members

### Main

| Members        | Type     | Description                                                                                                                                                                                                                    |
|----------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Author         | Required | The author of the Package. This string will be displayed to the user in Creator Central Widget Store.                                                                                                                          |
| Description    | Required | Provides a general description of what the package does. This string will be displayed to the user in Creator Central Widget Store.                                                                                            |
| Name           | Required | The name of the Package. This string will be displayed to the user in the Widget List and Creator Central Widget Store both.                                                                                                   |
| UUID           | Required | This is a unique identifier used to identify the package. See [Package Unique Identifier](Architecture.md#package-unique-identifier).                                                                                          |
| Icon           | Required | The relative path to a PNG image. This image will be displayed to the user in the Widget List and Creator Central Widget Store both. The Recommended image size is 75 x 54 in pixel. Creator Central supports PNG and SVG now. |
| URL            | Optional | A site to provide more information about the package.                                                                                                                                                                          |
| Version        | Required | Package's semantic version (1.0.0).                                                                                                                                                                                            |
| Runtime        | Required | Package executable file and platform information. See [Runtime](#runtime).                                                                                                                                                     |
| CreatorCentral | Required | Minimal supported Creator Central App version and SDK version of this Package. See [CreatorCentral](#creatorcentral).                                                                                                          |
| Widgets        | Required | An array of widgets in this Package. One Package can have one or multiple widgets. See [Widgets](#widgets).                                                                                                                    |


### Runtime

The relative path to the HTML/binary file containing the package code.

| Member | Type     | Description      |
|--------|----------|------------------|
| mac    | Required | macOS platform   |
| win    | Required | Windows platform |

Each platform needs to specify its executable files and platform requirements.
A web application will be loaded into an internal Chromium-based browser instance and a binary application will be started in the background.

| Member         | Type     | Description                                                            |
|----------------|----------|------------------------------------------------------------------------|
| Type           | Required | The type of the package executable. <ul><li>web</li><li>bin</li></ul>  |
| Target         | Required | The relative path to the HTML/binary file containing the package code. |
| MinimumVersion | Required | The minimum version of platform.                                       |


### CreatorCentral

Package can list its minimal supported version of Creator Central App version and SDK version.

| Member         | Type     | Description                             |
|----------------|----------|-----------------------------------------|
| MinimumVersion | Required | The minimum version of Creator Central. |
| SDKVersion     | Required | The current SDK version is 2.           |


### Widgets

One Package can have one or multiple widgets. For example, our [NumberToolbox](https://github.com/AVerMedia-Technologies-Inc/NumberToolbox) sample has 2 widgets: *Count* and *Random*.

| Member             | Type     | Description                                                                                                                                                                           |
|--------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name               | Required | The name of the widget. This string will be displayed to the user in the Widget List.                                                                                                 |
| Icon               | Required | Widget icon resource file path. This icon will be displayed to the user in the Widget List. The Recommended image size is 75 x 54 in pixel. Creator Central supports PNG and SVG now. |
| Tooltip            | Optional | The string is displayed as a tooltip when the user leaves the mouse over your widget in the Widget List.                                                                              |
| UUID               | Required | The unique identifier of the widget. See [Package Unique Identifier](Architecture.md#package-unique-identifier) as well.                                                              |
| PropertyViewPath   | Optional | The relative path to the Property View HTML file. If missing, the widget will have no Property View.                                                                                  |
| TitleEditable      | Optional | Indicates if the Widget title can be changed by user. False is read-only. Default value is true.                                                                                      |
| TitleViewEditable  | Optional | Indicates if the Widget title style can be changed by user. False is read-only. Default value is true.                                                                                |
| IconEditable       | Optional | Indicates if the Widget icon can be changed by user. False is read-only. Default value is true.                                                                                       |
| States             | Required | Specifies an array of states. See [States](#states).                                                                                                                                  |
| Layouts            | Optional | Specifies an array of layouts. See [Layouts](#layouts). If no layout information is provided, the widget will be treated as a 1 * 1 sized.                                            |


#### States

Each widget can have one or more states. For example, the Switch widget can have two states, ON and OFF.
The package can send a [changeState](EventsSent.md#change-widget-state) event.

| Member | Type     | Description                                                                                                                |
|--------|----------|----------------------------------------------------------------------------------------------------------------------------|
| Image  | Required | The default image for the state. The Recommended image size is 75 x 54 in pixel. Creator Central supports PNG and SVG now. |
| Name   | Optional | The default name of the state.                                                                                             |


#### Layouts

Creator Central supports multiple layouts defined by widgets in the package to meet functional needs.
The unit of width and height is a grid on the panel. The total size of the panel is a 5 * 4 grid.
This means you can use sizes from 1 * 1 to 5 * 4 to design your widgets to meet specific functional needs.

| Members | Type     | Description                                                                             |
|---------|----------|-----------------------------------------------------------------------------------------|
| Title   | Required | The string will be shown on Widget List.                                                |
| Icon    | Required | The image will be shown on Widget List. The recommend image size is 120 x 120 in pixel. |
| Width   | Required | The width of display view in grid. Maximum is 5.                                        |
| Height  | Required | The height of display view in grid. Maximum is 4.                                       |

The reference grid size is listed as below.

| Grid | Width | Height |
|:----:|:-----:|:------:|
|  1   |  150  |  108   |
|  2   |  308  |  224   |
|  3   |  466  |  340   |
|  4   |  624  |  456   |
|  5   |  782  |  ---   |

If no layout information is provided, the widget will be treated as a 1 * 1 sized.
