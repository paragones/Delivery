**Registering Things**

Once you have a `DeviceInfo`, you can register the Thing on the Geeny Cloud and retrieve a `BleThing` (a combination of device and cloud data):

```kotlin 
    sdk.geeny.register(clientInfo: DeviceInfo)
                .subscribeOn(ioScheduler)
                .observeOn(mainScheduler)
                .subscribe(doSomethingwith(thing))
```

At any later time you can get this information back with the serialNumber:

```kotlin 
    serialnumber = getSerialNumberFromYourPersistentToolOfYourChoice 
    sdk.geeny.get(serialNumber)
                .subscribeOn(ioScheduler)
                .observeOn(mainScheduler)
                .subscribe(doSomethingWith(thing))
```
