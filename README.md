# Geeny Android SDK
![Status](https://img.shields.io/badge/status-alpha-orange.svg?style=flat)
![Kotlin version](https://img.shields.io/badge/kotlin-1.1.4-blue.svg?style=flat)
![License](https://img.shields.io/badge/license-MPLv2-orange.svg?style=flat)

The Geeny Android SDK is a collection of libraries that help iOS developers to develop apps that work with the Geeny platform. The SDK is accompanied by an example app which demonstrates its functionalities.

Currently, the Android SDK contains the Router SDK.

## Geeny Gateway SDK

On a high level, the Router SDK allows an Android app to become a relay between a "non-IP-enabled Thing" and the Geeny platform. It enables such a Thing to be registered with the Geeny Cloud and securely transfer data to and from the Geeny MQTT endpoint.

At this stage, we require the Things to be "Geeny-native".

### Beta notice

This SDK is still under development and is currently released as Beta. Although it has been tested,, bugs and issues may be present. Some code might require cleanup. In addition, until version 1.0 is released, we cannot guarantee that API calls will not break from one SDK version to the next. Be sure to consult the Change Log for any breaking changes / additions to the SDK.

### Glossary:

* **Thing**: A connected device that can send and receive data - a fitness tracker or a smart lamp.
* **Non-IP-enabled Thing**: A cloudThingInfo which does not connect directly to the Internet by design (for example, it does not have a WIFI module built in). These Things are usually low-powered.
* **Geeny-enabled Thing**: A Thing that is compliant with the Geeny Thing specs.
* **ThingInfo**: Metadata of a Thing. Represents all metadata of a Thing, including its identifier, the characteristics and Geeny Thing Info.
* **Virtual Thing**: a Thing that is fully managed by a developer and connected to the Geeny SDK manually - e.g. a HomeKit appliance or HealthKit Data

### Requirements

* Andrioid Studio.
* An Android device running minSdkVersion 18 or higher. Tested on Sony Xperia Z5. Bluetooth is not supported in Simulator; thus, a real device is needed.
* A "Geeny-native" Bluetooth LE Thing for testing the automatic data publishing. For example, the [nRF52 DK](https://www.nordicsemi.com/eng/Products/Bluetooth-low-energy/nRF52-DK). See [How to Use the App](pages/HowToUse.md).
* Alternatively, you can create a [virtual Thing](pages/Adding%20Virtual%20Things.md). 
* To integrate Geeny Android SDK into your Android Studio project using Gradle, put the dependency under dependencies in your build.gradle:
        
        compile 'io.geeny.sdk:android:x.y.z'


#More Information
Please see the following contents below for some instructions and tutorials on how to use the app.
* [Registering Your IoT Devices](pages/RegisterDevice.md)
* [How to use the app](pages/HowToUse.md)
* [Setting up the App](pages/SetUp.md)
* [Running the Example App](pages/RunApp.md)
* [User Login](pages/UserLogin.md)
* [Adding Things](pages/AddingThings.md)

## Android API documentation (to come)

The complete API documentation of the Geeny Android SDK is available in: `<repoRoot>/GeenyGateway/Docs` (to come)

The documentation can also be generated locally using ... (to come).


## Not implemented yet - Coming soon

*  Background networking support and documentation
*  Automatic reconnection to registered Things
*  Complete unit test coverage of public methods 
*  Examples for using HealthKit and HomeKit devices as Things
*  Repeated scan and characteristic discovery should cancel previous tasks
*  Offline handling when the Thing itself or the Geeny API are unreacheable


## License

Copyright (C) 2017 Telefónica Germany Next GmbH, Charlottenstrasse 4, 10969 Berlin.

This project is licensed under the terms of the [Mozilla Public License Version 2.0](LICENSE.md).
