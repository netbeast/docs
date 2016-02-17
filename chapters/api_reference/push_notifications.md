# Push notifications to the user

Respond to an IoT event or a user action with a mobile or browser notification:
 
```javascript
var netbeast = require('netbeast')
netbeast.info('Something happened!')
netbeast.error('Something crashed!')
netbeast.warning('Something may crash next time!')
netbeast.success('Voi-la')
```

## Directly through MQTT
Netbeast router uses MQTT for notifications and real time messaging. It is the preferred language for sensors and its exposed API is rather simple. If you are already using [mqtt.js](https://www.npmjs.com/package/mqtt) you can send notifications without [Netbeast API module](http://github.com/netbeast/api) easily.

```javascript
var mqtt = require('mqtt')
var client = mqtt.connect('10.0.0.1') // Netbeast IP in your subnet
const msg = {title: "my app", body: "An error has occurred", emphasis: "error"}
client.publish('netbeast/push', JSON.stringify(msg))
```

A notification is a extensible JSON object carrying at least the field body. All options below:

```javascript
{
 body: "The notification message content",
 title: "By default, app name or `dashboard`, it is the heading of the toastr",
 icon: url, // Not yet ready, but in the future will work with browser native and mobile native notifications
 emphasis: "success|warning|error|info",
 timeout: "3000" // time in ms – default is never
}
```

For a deeper view, take a look on notifications utility implemented on dashboard https://github.com/netbeast/dashboard/blob/master/src/helpers/broker.js