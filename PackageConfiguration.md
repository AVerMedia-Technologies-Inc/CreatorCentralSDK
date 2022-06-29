Package Configuration
===


## PackageConfig.json Example

Here is an example of PackageConfig.json file. Developers should modify the fields for your Package/Widget.

``` json 
{
    "Author": "AVerMedia",
    "Description": "This kit includes two display types of lighting effects, allowing users to choose according to the space and the required information.",
    "Name": "AX Lighting EFX",
    "UUID": "com.avermedia.package.lighting.toolbox",
    "Icon": "images/packageAxLightingIcon",
    "URL": "https://www.avermedia.com/gaming/creatorcentral",
    "Version": "1.0.0",
    "Runtime": {
        "mac": {
            "type": "bin",
            "target": "AXLighting",
            "MinimumVersion": "11.0"
        },
        "win": {
            "type": "bin",
            "target": "AXLighting",
            "MinimumVersion": "11.0"
        }
    },
    "CreatorCentral": {
        "MinimumVersion": "1.1",
        "SDKVersion": 2
    },
    "Widgets": [
        {
            "Name": "Turn on/off AX lighting effects.",
            "Icon": "images/toggleIcon",
            "Tooltip": "Turn on/off AX lighting effects.",
            "UUID": "com.avermedia.axlighting.toggle",
            "PropertyViewPath": "property/index1.html",
            "States": [
                {
                    "Image": "images/fullIcon",
                    "Title": "On"
                },
                {
                    "Image": "images/liteIcon",
                    "Title": "Off"
                }
            ],
            "Layouts": [
                {
                    "Title": "Full",
                    "Icon": "images/fullLayoutIcon",
                    "Width": 4,
                    "Height": 3
                },
                {
                    "Title": "Lite",
                    "Icon": "images/liteLayoutIcon",
                    "Width": 1,
                    "Height": 2
                }
            ]
        },
        {
            "Name": "Set AX Lighting Effect Mode.",
            "Icon": "images/modeIcon",
            "Tooltip": "Switch the lighting effect mode of AX.",
            "UUID": "com.avermedia.axlighting.mode",
            "PropertyViewPath": "property/index2.html",
            "States": [
                {
                    "Image": "images/01",
                    "Title": "Stream"
                },
                {
                    "Image": "images/02",
                    "Title": "Record"
                }
            ],
            "Layouts": [
                {
                    "Title": "Full",
                    "Icon": "images/fullIcon",
                    "Width": 2,
                    "Height": 2
                },
                {
                    "Title": "Lite",
                    "Icon": "images/liteIcon",
                    "Width": 1,
                    "Height": 4
                }
            ]
        }
    ]
}

```


## Members

### Main

| Members        | Type     | Description|
| - | - | - |
| Widgets        | Required | An array of widgets in this Package. One Package can have one or multiple widgets. For example, the Stream Live package can contain 3 widgets: Set Current Scene, Set Current Source, and Start to Record|
| Author         | Required | The author of the Package. This string will be displayed to the user in Creator Central Widget Store.|
| Description    | Required | Provides a general description of what the package does. This string will be displayed to the user in Creator Central Widget Store.|
| Name           | Required | The name of the package. This string will be displayed to the user in the Widget List and Creator Central Widget Store both.|
| UUID | Required | This is a unique identifier used to identify the package. The unique identifier must be contained only lowercase alphanumeric characters(a-z, 0-9), hyphen(-), and period(.). We strongly suggest to name your identifier in **reverse-DNS** format. For example, a **System** package made by AVerMedia(avermedia.com). We suggest to use **com.avermedia.system** as the unique identifier. |
| Icon | Required | The relative path to a PNG image. This image will be displayed to the user in the Widget List and Creator Central Widget Store both. The Recommended image size is 75 x 54 in pixel. |
| URL | Optional | A site to provide more information about the package.|
| Version | Required | Package's semantic version (1.0.0)|
| Runtime | Required | The relative path to the HTML/binary file containing the package code.|
| CreatorCentral | Required | Minimal supported Creator Central App version and SDK version  of this Package. |


### Widgets

| Member   | Type     | Description |
| -------- | -------- | ----------- |
| Icon     | Required | The relative path to a PNG image. This image will be displayed to the user in the Widget List. The Recommended image size is 75 x 54 in pixel. |
| Name     | Required | The name of the widget. This string will be displayed to the user in the Widget List. |
| States   | Required | Each widget can have one or more states. For example, the Mute widget may have two states, mute and unmute. Ask the action to change its state by sending a changeState event. |
| Layouts   | Optional | Specifies an array of layouts. Each widget can have one or more layouts. For example, the Clock widget can have two different layouts. One is analog and another is digital. |
| Tooltip  | Optional | The string is displayed as a tooltip when the user leaves the mouse over your widget in the Widget List. |
| UUID | Required | The unique identifier must be contained only lowercase alphanumeric characters(a-z, 0-9), hyphen(-), and period(.). We strongly suggest to name your identifier in **reverse-DNS** format. For example, a **Lighting Toggle** widget made by AVerMedia(avermedia.com). We will use **com.avermedia.axlighting.toggle** as the unique identifier.  |
| PropertyViewPath | Optional | The relative path to the Property View HTML file. If missing, the widget will have an empty Property View. |


### States

| Member | Type     | Description                      |
| ------ | -------- | -------------------------------- |
| Image  | Required | The default image for the state. The Recommended image size is 75 x 54 in pixel. |


### Layouts

Creator Central supports multiple layouts defined by widgets in the package to meet functional needs. The unit of width and height is a grid on the panel. The total size of the panel is a 5 * 4 grid. This means you can use sizes from 1 * 1 to 5 * 4 to design your widgets to meet specific functional needs. The reference image size is list as below.

| Grid | Width \* Height |
| 1x1 | 150 \* 108 |
| 2x1 | 308 \* 108 |
| 2x2 | 308 \* 224 |
| 2x4 | 308 \* 456 |
| 3x4 | 466 \* 456 |
| 4x3 | 624 \* 340 |
| 5x4 | 782 \* 456 |  

| Members | Type | Description |
| - | - | - |
| Title | Required | The string will be shown on Widget List. |
| Icon | Required | The image will be shown on Widget List. The recommend image size is 120 x 120 in pixel. |
| Width  | Required | The width of display view in grid.  |
| Height | Required | The height of display view in grid. | 

### Runtime

| Member         | Type     | Description                                                            |
| -------------- | -------- | ---------------------------------------------------------------------- |
| mac / win      | Required | The name of the platform, mac or win                                   |
| Type           | Required | The type of the package executable, web or bin                         |
| Target         | Required | The relative path to the HTML/binary file containing the package code. |
| MinimumVersion | Required | The minimum version of platform. |

### CreatorCentral

| Member         | Type     | Description                             |
| -------------- | -------- | --------------------------------------- |
| MinimumVersion | Required | The minimum version of Creator Central. |
| SDKVersion     | Required | The current SDK version is 2.           |

