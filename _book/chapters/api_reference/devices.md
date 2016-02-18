# Devices

This object include useful methods for managing different aspects of the Smart devices

#### devices.group(name , devicesId)####
This function allows us to make group of devices. The argument name defines the group name. DevicesId will be an array of ids of the devices that should be grouped.

```javascript
var nb = require('netbeast')

var args = [1, 3, 7]

nb.devices().group('roof', args)
.then(function (data) {}
.catch(function (error) {}
```

#### devices.discover([brandName])

This function allows us to activate the discovery process. With the brand-name parameter you can specify a concrete app (like belkin-wemo, philips-hue). If you don´t include this argument, the discovery will be apply to all available brands.

```javascript
var nb = require('netbeast')

nb.devices().discovery('belkin-wemo')
.then(function (data) {}
.catch(function (error) {}
```