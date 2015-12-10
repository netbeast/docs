# Resources

A resource contain information about every smart device connected through the dashboard. It has the following fields:

Property    |  Description  |   Values  |   Default
------------|---------------|-----------|----------
id          | Identifies the resource in the db | Integer (automatic) | -
app         | show the device brand | String (belkin-wemo, philips-hue) | -
location    | Location of the devices in the house | String (up to developer) | none
topic       | Define the device field of actuation | String (lights.bridge,switch) | -
group       | Resources can be grouped | String (up to developer) | none

Resources has methods for:
*   Obtain the current state of devices, for expample
````javascript
resources('lights').get()
````
*   Change the current state of devices, for example
````javascript
resources('switch').set({power: true})
````
*   Select a device through its group or location, for example
````javascript
resources('lights').at('kitchen').get('brightness')
````

####resources([topic]).at(location).METHOD

This method allows us to select a group of devices form a specific location. It can´t be used alone and should be follow by other method.

````javascript
var nb = require('netbeast')

nb.resources('lights').at('bedroom').get()
.then(function (data) {}
.catch(function (error) {}
````


In this example, we get information about all the lights placed at the kitchen. 

#### resources([topic]).delete([args])

The delete method allow us to remove resources from the database. You can use an argument (args: json object) for this method that select an specific property of devices.

````javascript
var nb = require('netbeast')

// Remove all the lights
nb.resources('lights').delete()
.then(function (data) {}
.catch(function (error) {}

// Remove all the belkin-wemo lights group by 'colorful'

var args = { app: 'belkin-wemo'}

nb.resources('lights').groupBy('colorful').delete(args)
.then(function (data) {}
.catch(function (error) {}
````

#### resources([topic]).deleteById(id)

The deleteById method allows us to remove resources from the database. With the id argument we select a specific device from the db.

````javascript
var nb = require('netbeast')

nb.resources().deleteById(1)
.then(function (data) {}
.catch(function (error) {}
````

The topic is useless on this method.

#### resources([topic]).get([value])

The get method allows us to obtain information about the current state of the devices. You can obtain all the data about the state or specify a concrete value.

````javascript
var nb = require('netbeast')

// Returns the state of all lights
nb.resources('lights').get()
.then(function (data) {}
.catch(function (error) {}

// Returns the brightness of all the lights
var nb = require('netbeast')

nb.resources('lights').get('brightness')
.then(function (data) {}
.catch(function (error) {}
````
 You can only ask for one value.  nb.resources('lights').get('power', 'brightness') is not allowed.

### resources([topic]).getById(id)

The getById method allows us to get information about the current state of the devices. You will receive all the information of the specified device.

````javascript
var nb = require('netbeast')

nb.resources().getById(1)
.then(function (data) {}
.catch(function (error) {}
````

The topic is useless on this method.

#### resources([topic]).groupBy(name).METHOD

This method allows us to select devices form a specific group. It can´t be used alone and should be follow by other method.

````javascript
var nb = require('netbeast')

nb.resources('lights').groupBy('roof').set({power: true})
.then(function (data) {}
.catch(function (error) {}
````

In this example, we switch all the lights of the group ‘roof’ on. 

#### resources([topic]).set(args)

The set method allows us to change the current state of the devices. You can modify different values at the same time.

````javascript
var nb = require('netbeast')

// Change the brightness of all lights
nb.resources('lights').set({brightness: 100})
.then(function (data) {}
.catch(function (error) {}

//  Change the brightness and color of all the lights
var nb = require('netbeast')

nb.resources('lights').set({brightness: 80, hue: 350, saturation: 100})
.then(function (data) {}
.catch(function (error) {}
````

####resources([topic]). setById(id, args)

The setById method allows us to change the current state of the given device. You can modify different values of the specified device.

````javascript
var nb = require('netbeast')

var args = { power: 'on', brightness: 50 }

nb.resources().setById(1, args)
.then(function (data) {}
.catch(function (error) {}
````

The topic is useless on this method.