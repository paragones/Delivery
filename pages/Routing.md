**Routing**

With the `BleThing` you can get a list `GeenyFlow` that contains all the routes, that you registered for.


```kotlin 
    serialnumber = getSerialNumberFromYourPersistentSourceOfYourChoice 
    sdk.geeny.get(serialNumber)
                .subscribeOn(ioScheduler)
                .observeOn(mainScheduler)
                .subscribe(doSomethingWith(geenyFlow))
```

The GeenyFlow consists of a list of `Route`. A `Route` can e.g. send values from a bluetooth notify characteristic to
the broker. And another route picking up that message and sending it to the Geeny MqttServer. To understand what a particular route is
doing you can ask for the RouteInfo.

```kotlin 
    route = geenyFlow.routes[0]
    routeInfo = route.info() 
    
    RouteInfo(
        type                    // (RouteType) can be BLE, MQTT, CUSTOM
        direction               // (Direction) can be PRODUCER or CONSUMER
        topic                   // (String) the id of the storage on the broker
        val clientIdentifier    // (String) the identifier of the client, e.g. in BleClient it will be the mac adress
        val clientResourceId    // (String) the identifier of the resource on the client, e.g. in BleClient it will be the charactersticId
    )
```

You can start and stop a route by:

```kotlin 
    route.start()
    route.stop()
```

This will initiate a connection attempt to Ble/Mqtt and once successful start producing/consuming messages. You can always
check the state of the route (e.g a BleClient that disonnects will stop the route):

```kotlin 
    route.isRunning()
    ...or in a streaming fashion
     
    route.running().subscribe{doSomethingWith(connectionState)}
```
