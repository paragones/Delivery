### User Login

Before a user can send and receive data from the Geeny Cloud, they have to log in into their [Geeny account]((https://labs.geeny.io/login)).

Request the username and the password from the user and pass them on to the `Gateway.shared.login()` method:


KOTLIN & JAVA
 ```kotlin
    sdk.geeny.auth.signInWithCredentials(c)
                         .subscribeOn(ioScheduler)
                         .observeOn(mainScheduler)
                         .subscribe(
                                 { e.g.: openMain... },
                                 { e.g.: showError...}
                         )
 ```
You can always check if the user is logged in by looking at the `isLoggedIn` property:

KOTLIN & JAVA
```kotlin
        sdk.geeny.auth.isSignedIn()
                .subscribeOn(ioScheduler)
                .observeOn(mainScheduler)
                .subscribe { booleanState ->
                    if (booleanState) {
                        e.g.: openMain....
                    } else {
                        e.g.: openSignIn...
                    }
                }
```

And of course logout:

```kotlin
        sdk.geeny.auth.signOut()
                .subscribeOn(ioScheduler)
                .observeOn(mainScheduler)
                .subscribe { 
                        e.g.: openSignIn...  
                    
                }
```

