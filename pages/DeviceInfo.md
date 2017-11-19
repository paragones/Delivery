**Device Info**

Scanning results returns an array of `[BleClient]`, this object provides different information. Some of them
are directly accessible, other need a connection first or the information are streamed in an Observable as
they might change and/or not accessible until a successful connection. 

Before connection and registration:

```kotlin
    client.address() // the mac address of the bluetooth client 
    client.name() // the name of the ble device
    client.isGeenyDevice() // indeicates if it has a gatt service with the Geeny UUID
```

After connection:

```kotlin
    client.connection()             // returns an Observable of type ConnectionState to track the connection state of the device
    client.geenyInformation()       //returns an Observable of type DeviceInfo to track additional geeny related infos after connection
```

The information a DeviceInfo provides:

```kotlin
    DeviceInfo(
        deviceName,                  // (String) value representing the name of the device,
        address,                     // (String) value representing the ble mac address
        protocolVersion,             // (Int) value representing the protocol version this cloudThingInfo communicates
        serialNumber,                // (UUID) value representing the serial number
        thingTypeId                 // (UUID) value representing the thingtype registerd at Geeny
    )
```
