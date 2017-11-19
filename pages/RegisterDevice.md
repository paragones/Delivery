### Registering Your IoT Devices
Before you use the app, make sure you have done the following registration:
1. Make sure you have created your own [Geeny Account](https://labs.geeny.io/login)

2. Follow the 3 steps in [Getting Started with Devices](https://docs.geeny.io/getting-started/devices/)
- *Note: Don't forget to save your <b>token</b>. It will be used for sending messages through the SDK*

3. Create and Register your Message Types.
- Go to Swagger UI link for [Creating and Registering Message Types (MT)](https://labs.geeny.io/things/docs/index.html#!/MessageTypes/post_things_api_v1_messageTypes)
- Input your token at the <b><i>authorization input field</b></i> as `JWT <your-token>`
- At the <b><i>NewMessageType input field</b></i>, input the following JSON information: 
    - `name` - your MT Name 
    - `media_type` - your MT Type
    - `description` - your MT Short Description
    - `full_description` - your MT Full Description
    - `documentation_url` - your MT documentation URL
    - `data_sample` - your MT data sample such as temperature, humidity, wind speed, etc..
    - `tags` - your MT tags
    - JSON Sample:
        ```json 
        {
          "name": "Instantaneous Humidity Value", 
          "media_type": "application/cbor",
          "description": "Instantaneous Humidity Value",
          "full_description": "BRAND, the industry-leader sensor manufacturer, brings you Temperature Sensor 3000",
          "documentation_url": "http://path.to/documentation",
          "data_sample": "{\"temperature\": 21, \"unit\": \"celcius\"}",
          "tags": [
            "humidity",
            "sensor",
            "Brand"
          ]
        }
        ```
    - Click the `TRY IT OUT BUTTON`
    - You should get a sample response below, if every information inputted was correct:
        ```json
        {
             "description": "Instantaneous Humidity Value",
             "media_type": "application/cbor",
             "tags": [
               "humidity",
               "sensor",
               "Brand"
             ],
             "name": "Test Message Type 1",
             "created": "2017-11-18T16:55:32.586Z",
             "id": "e894bb32-f339-4073-b7ae-94b147019510",
             "owner": "281bd338-4356-4c7b-a683-bbe00b99032d"
        }
        ```
    - You have now created and registered a new Message Type. The <b><i>id</b></i> created is your `messageId`. Save it.
4. Create and Register your Thing Types
- Go to Swagger UI link for [Creating and Registering Thing Types](https://labs.geeny.io/things/docs/index.html#!/ThingTypes/post_things_api_v1_thingTypes)
- Input your token at the <b><i>authorization input field</b></i> as `JWT <your-token>`
- At the <b><i>NewMessageType input field</b></i>, input the following JSON information: 
    - `name` - your Thing Type (TT) Name 
    - `description` - your TT Short Description
    - `full_description` - your TT Full Description
    - `documentation_url` - your TT documentation URL
    - `resources` - resources should contain two objects that has two methods: `pub` and `sub`. 
    - `reources/uri` - the uri for the TT method
    - `method` - a type that would determine if your TT would be publishing or subscribing a message. 
    Write `pub` if your TT is to publish a message to the SDK. 
    Write `sub` if your TT is to subscribe a message from the SDK.
    
        *Note: You can also write only one class(that has either `pub` or `sub` methods) inside the resource list depending on your needs*
    - `message_type` - the Message Type Id you have created from the previous registration 
    - JSON Sample
        ```json
        {
          "name": "BRAND Humidity Sensor",
          "description": "BRAND Temperature Sensor 3000, as seen on TV",
          "full_description": "BRAND, the industry-leader sensor manufacturer, brings you Temperature Sensor 3000",
          "documentation_url": "http://path.to/documentation",
          "resources": [
            {
              "uri": "humidity/now",
              "method": "pub",
              "message_type": "e894bb32-f339-4073-b7ae-94b147019510"
            },
            {
              "uri": "humidity/yesterday",
              "method": "sub",
              "message_type": "e894bb32-f339-4073-b7ae-94b147019510"
            }
          ]
        }    
        ```
    - Click the `TRY IT OUT BUTTON`
    - You should get a sample response below, if every information inputted was correct:
        ```json
        {
          "name": "BRAND Humidity Sensor",
          "public": true,
          "created": "2017-11-18T17:17:26.613Z",
          "description": "BRAND Temperature Sensor 3000, as seen on TV",
          "id": "6a526c88-9dd7-4143-bd7e-6fc1f02909ee",
          "full_description": "BRAND, the industry-leader sensor manufacturer, brings you Temperature Sensor 3000",
          "owner": "281bd338-4356-4c7b-a683-bbe00b99032d",
          "documentation_url": "http://path.to/documentation"
        }
        ```
    - You have now created and registered a new Thing Type. The <b><i>id</b></i> created is your `thingTypeid`. Save it.
5. Get your Thing Type Resource Id
- Go to Swagger UI link for [Getting Thing Types Resource Id](https://labs.geeny.io/things/docs/index.html#!/ThingTypes/get_things_api_v1_thingTypes_id_resources)
- Input your `thingTypeid` at the <b><i>id input field</b></i>
- Click the `TRY IT OUT BUTTON`
- You should get a sample response below, if every information inputted was correct:
    ```json
    {
      "meta": {
        "offset": 0,
        "limit": 50
      },
      "data": [
        {
          "id": "668b180b-f709-4914-bcc9-6d9ae6d489b9",
          "uri": "humidity/now",
          "method": "pub",
          "message_type": "e894bb32-f339-4073-b7ae-94b147019510"
        },
        {
          "id": "a130c6f0-6bcd-47ee-b02e-2bf5d150b8f8",
          "uri": "humidity/yesterday",
          "method": "sub",
          "message_type": "e894bb32-f339-4073-b7ae-94b147019510"
        }
      ]
    }
    ```
- The two `id` inside the `data` are the Thing Type Resource Ids. Save them both. 

After you have done these steps, you are now ready to use the app! 