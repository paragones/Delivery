**Adding Virtual Things**

Write the following code in your Geeny Configuration:

KOTLIN
```kotlin
val sdk: GeenySdk by lazy {
     val config =
             GeenyConfiguration.Builder()
                     .withEnvironment(Environment.Type.PRODUCTION)
                     .withVirtualThing(
                             VirtualThing.Builder("Example Virtual", <your thingTypeId>, ThingTypeName)
                                     .withSlot(LogSink("Log", <your resourceSubId>, "SINK LOGGER"))
                                     .withSlot(FeedForward(<your resourcePubId>, "Feed Forward"))
                                     .build()
                     )
                     .build()
     GeenySdk.create(config, context)
 }
```

JAVA

```java
    public final GeenySdk sdk;
    public ApplicationComponent(Context context) {
        GeenyConfiguration config = new GeenyConfiguration.Builder()
                .withEnvironment(Environment.Type.PRODUCTION)
                .withVirtualThing(
                        new VirtualThing.Builder("Example Virtual", <your thingTypeId>, "DemoThing")
                                .withSlot(new LogSink("Logging Example", <your resourceSubId>, "LOG_TAG_EXAMPLE"))
                                .withSlot(new FeedForward(<your resourcePubId>, "Feed Forward Channel"))
                                .build()
                )
                .build();

        sdk = GeenySdk.Companion.create(config, context);
    }
```
- `Environment.Type.PRODUCTION` is the Environment where connections were setup for Geeny MQTT and Server
- `thingTypeId, resourceSubId, and resourcePubId` are the ids created when you [registered your device](pages/RegisterDevice.md)
- `LogSink` is an internal Logger for BLE
- `FeedForward` is a class intended to manage messages from the SDK to Geeny MQTT

On your activity/fragment, add the following classes and functions:

KOTLIN
```kotlin
class VirtualThingFragmentK : Fragment(), VirtualThingGateway.Callback {
    private fun app(): ApplicationComponent = DemoApp.from(context).component
    private fun sdk(): GeenySdk = app().sdk

    private lateinit var gateway: VirtualThingGateway
    private val client: Client? = sdk().getVirtualThing(ApplicationComponent.ThingTypeId /*Your Thing Type ID*/)
    private var flowViewMap: MutableMap<GeenyFlow, GeenyFlowView> = HashMap()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        gateway = sdk().getVirtualGateway(arguments.getString(ApplicationComponent.ThingTypeId /*Your Thing Type ID*/), app().mainScheduler)

        // Send a message to Geeny MQTT
        val messageChar = "hello"
        client?.let { c ->
            c.write(ClientMessage(
                    ApplicationComponent.ResourcePubId,
                    ByteArray(1).apply { set(0, messageChar.toByte()) }))
                    .subscribeOn(Schedulers.io())
                    .observeOn(AndroidSchedulers.mainThread())
                    .subscribe({ /*Log Messsage */ }, { /*Log Error*/ })
        }
    }

    override fun onCreateView(inflater: LayoutInflater?, container: ViewGroup?, savedInstanceState: Bundle?): View? =
            inflater?.inflate(R.layout.fragment_virtual_thing, container, false)

    override fun onStart() {
        super.onStart()
        gateway.attach(this)
    }

    override fun onStop() {
        gateway.detach()
        super.onStop()
    }

    override fun onDeviceIsNotRegisteredYet() {
        gateway.register()
    }
}
```

JAVA

```java
public final class VirtualThingFragmentK extends Fragment implements Callback {
   private VirtualThingGateway gateway;
   private final Client client;
   private Map flowViewMap = new HashMap();

   private final ApplicationComponent app() {
      return DemoApp.Companion.from(getContext()).getComponent();
   }

   private final GeenySdk sdk() {
      return app().getSdk();
   }

   public void onCreate( Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      String thingTypeId = getArguments().getString(ApplicationComponent.Companion.getThingTypeId());
      gateway = sdk().getVirtualGateway(thingTypeId, app().getMainScheduler());
      String messageChar = "hello";
      client = sdk().getVirtualThing(ApplicationComponent.ThingTypeId /*Your Thing Type ID*/);
	  
	  // Send a message to Geeny MQTT
      if(client != null) {
         String resourcePubId = ApplicationComponent.Companion.getResourcePubId();
         byte[] byteArray = new byte[1];
		         byteArray[0] = Byte.parseByte(messageChar);
         client.write(new ClientMessage(resourcePubId, byteArray))
                     .subscribeOn(Schedulers.io())
                     .observeOn(AndroidSchedulers.mainThread())
                     .subscribe({ /*Log Messsage */ }, { /*Log Error*/ });
      }

   }


   public View onCreateView( LayoutInflater inflater,  ViewGroup container,  Bundle savedInstanceState) {
      return inflater != null?inflater.inflate(R.layout.fragment_virtual_thing, container, false):null;
   }

   public void onStart() {
      super.onStart();
      gateway.attach((Callback)this);
   }

   public void onStop() {
      gateway.detach();
      super.onStop();
   }

   public void onDeviceIsNotRegisteredYet() {
      gateway.register();
   }
}
```
