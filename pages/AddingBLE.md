#### Adding Bluetooth LE Things

To speed up the integration process with Bluetooth LE connected devices, the Route SDK can fully take on the Bluetooth communication with the Thing. For this to work, the hardware provider must implement the Geeny BLE characteristic in the device firmware. This characteristic contains info such as the registered ThingType and the serial number of the device. The iOS GeenyGateway SDK will recognize this information, parse it and pass it on to the Cloud during the registration process.

**Scanning for Things**


```kotlin    
    sdk.clients.ble.availableDevices()
        .observeOn(mainScheduler)
            .subscribe{
                bleDevice -> e.g: update list
            }
            
    sdk.clients.ble.startScan()
    
    ... and then 
    
    sdk.clients.ble.stopScan()
    
```
