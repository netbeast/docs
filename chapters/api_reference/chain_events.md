# Events

With Netbeast API you can subscribe to a specific topic. Using this method you will
be notified when any device publish data about the given topic.

```javascript
var netbeast = require('netbeast')
netbeast.on('temperature', function (err, message) {
    // this function is called everytime temperature
    // event happens
    if (message.temperature > 30) {
        // do something
    }
})
```

For publishing data on the MQTT channels can use this.

```javascript
netbeast('humidity').publish({ humidity: 50 }) 
```

This is basically an usual subscription to a mqtt channel. If you feel more comfortable
using mqtt directly, it will looks something like that.

```javascript
var client = mqtt.connect('ws://NETBEAST_IP:PORT')

    client.on('connect', function () {
      client.subscribe('netbeast/' + topic)
    })

    client.on('message', function (topic, message) {
      if (message) {
        // do something
      }
    })

```
