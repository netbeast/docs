# devices.group(name, devicesId)

This function allows us to make group of devices. The argument name defines de group name. DevicesId will be an array of ids of the devices that should be grouped.

````javascript
var nb = require('netbeast')

var args = [1,3, 7 }

nb.devices().group('roof', args)
.then(function (data) {}
.catch(function (error) {}
````
