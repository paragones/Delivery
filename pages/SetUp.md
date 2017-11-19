### Set up

In your dependency tool or if you don't have on in your Application class add the GeenySdk as a dependency.
You need a configuration file first. 

KOTLIN
 ```kotlin
    
    val sdk: GeenySdk by lazy {
        val config = GeenyConfiguration.Builder().build()
        GeenySdk.create(config, context.applicationContext)
    }
 
 ```
 JAVA
 ```java
    GeenyConfiguration config = GeenyConfiguration.Builder().build()
    GeenySdk sdk = GeenySdk.create(config, context.applicationContext)
 ```
 

Then you can initialize the GeenySdk in a launching activity by calling:

KOTLIN
 ```kotlin
    sdk.init().subscribe(
        {Log.d(TAG, it.toString())},
        {Log.e(TAG, it.message, it)}
    )
 ```
 JAVA
 ```java
    sdk.init().subscribe(
        {sdkInitializationResult -> Log.d(TAG, it.toString())},
        {error -> Log.e(TAG, error.message, error)}
    )
 ```
