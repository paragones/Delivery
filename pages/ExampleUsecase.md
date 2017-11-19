**Example Usecase**

The SDK provides an example usecase for connecting a registered Geeny device. If you have a bluetooth mac address and the Android main
RXScheduler you can get a BleGateway by:


```kotlin 
    gateway = getBleGateway(bluetoothAdress, mainScheduler)
```

The gateway provides a callback interface:

KOTLIN

```kotlin 
    interface Callback {
        fun onClientLoaded(client: BleClient)
        fun onConnectionStateHasChanged(connectionState: ConnectionState)
        fun onDeviceInfoLoad(clientInfo: DeviceInfo)
        fun onDeviceIsNotRegisteredYet()
        fun onFlowsLoaded(flows: List<GeenyFlow>)
        fun onRouteConnectionStatusHasChanged(flow: GeenyFlow, route: Route, status: ConnectionState)
        fun progress(show: Boolean)
        fun onError(throwable: Throwable)
        fun onValueHasChanged(flow: GeenyFlow, bytes: ByteArray)
    }
```

JAVA

```kotlin 
    interface Callback {
        void onClientLoaded(BleClient client)
        void onConnectionStateHasChanged(ConnectionState connectionState)
        void onDeviceInfoLoad(DeviceInfo clientInfo)
        void onDeviceIsNotRegisteredYet()
        void onFlowsLoaded(List<GeenyFlow> flows)
        void onRouteConnectionStatusHasChanged(GeenyFlow flow, Route route, ConnectionState status)
        void progress(boolean show)
        void onError(Throwable throwable)
        void onValueHasChanged(GeenyFlow flow, byte[] bytes)
    }
```

You can attach this callback by

KOTLIN 

```kotlin
    callback = object: BleGateway.Callback {...}
    gateway.attach(callback)
```
JAVA

```kotlin
    callback = new BleGateway.Callback() {...}
    gateway.attach(callback)
```

Don't forget to detach by calling:

```kotlin
    gateway.detach()
```

Then you can interact with the gateway by:


```kotlin
    gateway.connect(context)                // connects the ble device
    gateway.disconnect()                    // disconnects the ble device
    gateway.register()                      // register this device
    gateway.triggerRead(clientResourceId)   // triggers read on characteristic
    gateway.start(flow, context)            // once you have the flows you can start them by
```
