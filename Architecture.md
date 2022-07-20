# Architecture

## Overview

Creator Central is a utility application that helps you manage your AX devices.
It loads all the custom packages when the application starts.

WebSocket APIs allow bidirectional communication between the packages and the Creator Central application using JSON.
<br/>
<div align="center">
	<img src="images/01_architecture.jpg" style="zoom:80%"/>
</div>
<br/>

### Package Registration

Creator Central will provide a specific WebSocket port to the Package.
A Package must follow the [Registration Flow](RegistrationFlow.md) to establish the bidirectional communication between Creator Central and itself.


### Key Events

Only one instance of the Package will be executed by Creator Central.
When multiple widgets in the same package are running in Panel, the Package must handle all events by the identifier in them.
Those events include user [press down](EventsReceived.md#action-down)/[press up](EventsReceived.md#action-up), [widget triggered](EventsReceived.md#action-triggered) on AX devices, etc.

### Cross Platform

Creator Central is an application that runs on Windows and macOS, So it supports cross-platform packages for Windows and macOS.
These packages can be executables written in JavaScript, C++ or other programming languages.

## Package
<br/>
<div align="center">
	<img src="images/02_package_components.jpg" style="zoom:80%"/>
</div>
<br/>

A package is composed of 4 parts:

- PackageConfig.json: describes the package (name, author, icon, etc.) and defines the widgets
- Runtime: the runtime instance executed on startup. It controls the main business logic and updates the display content.
- Property View: user configurations to the widget (if necessary)
- Resources: images, etc.

The [PackageConfig.json](PackageConfiguration.md) file has a Runtime member indicating the path to the plugin's executable instance.
Please read the document for more detail information.

An HTML file (in case you use JavaScript) or a compiled command-line tool (C++, Objective-C, C#, ...) to run in a separate process.

### Package Unique Identifier

Every Package must have a unique identifier in Creator Central.
The unique identifier must be contained only lowercase **alphanumeric characters**(a-z, 0-9), **hyphen**(-), and **period**(.).
We strongly suggest to name your identifier in **reverse-DNS** format.

For example, a **Hello World** package made by AVerMedia(avermedia.com).
We will use `com.avermedia.helloworld` as the unique identifier of this Hello World package.
This package has a **Morning** widget, so we can name it `com.avermedia.helloworld.morning`.


### Package Instance

Each package is a single instance in Creator Central. In other words, your app will be launched once and one time only.

When Creator Central launches your app, you can [receive events](EventsReceived.md) in your app instance.
A package instance can also [send events](EventsSent.md) to Creator Central. Make sure you read the documents.

Each widget instance has its [context](#context) and maintained by Creator Central.
Even you have only one widget in your package, a user may drag multiple instances to Creator Central Panel.
Remember each widget may have its own configurations so make sure you can handle them well.

You can also use [setPackageSettings](EventsSent.md#set-package-settings) to save some data globally for the package (third-party access key, user settings, etc.).

## Widgets

A package can have one or multiple widgets in its [Package Configuration](PackageConfiguration.md).
Developers must define these widgets correctly for Creator Central.
Please read the documents or check our [samples](Samples.md).

Each Widget must also have its own Unique Identifier for the Creator Central application to identify widgets in the same package.
We strongly suggest to name your identifier in **reverse-DNS** format.
You can follow the [same rule](#package-unique-identifier) for the Package.

### Context

Creator Central will give every widget a `context` and will use it to identify them.
Please note that it is different from its own identifier defined in [Package Configuration](PackageConfiguration.md).

## Property View

A Property View is a HTML5 webpage and designed to be a configuration panel for a Widget.
Creator Central will load your property view page in a Chromium-based browser container.

Developers must follow the [Registration Flow](RegistrationFlow.md#property-view-registration) to establish the communication to Creator Central.
Once the bidirectional communications are established successfully, a Property View page can use [sendToPackage](EventsSent.md#send-to-package) to send messages to the Package.
The Package can also use [sendToPropertyView](EventsSent.md#send-to-property-view) to communicate with the Property View.

When the Property View is displayed, a [didReceiveWidgetSettings](EventsReceived.md#on-widget-settings-arrived) event will be given.
The Property View can use this information to display its settings in its webpage.

You can use [setWidgetSettings](EventsSent.md#set-widget-settings) to save settings for the widget's instance persistently.
The package will also automatically receive a [didReceiveWidgetSettings](EventsReceived.md#on-widget-settings-arrived) event with the new settings.

You can also use [setPackageSettings](EventsSent.md#set-package-settings) to save some data globally for the package (third-party access key, user settings, etc.).
But we recommend you to only use this in your Package.
