# Resources

Netbeast API has methods for manage the smart devices stored on the Resources DB. With Netbeast we can:
*   Obtain the current state of devices, for example
````javascript
netbeast('lights').get()
````
*   Change the current state of devices, for example
````javascript
netbeast('switch').set({power: true})
````
*   Select a device through its group or location, for example
````javascript
netbeast('music').at('kitchen').get('track')
netbeast('music').groupBy('color-white').get('track')
````

Index:

* [.at()](#at)
* [.create()](#create)
* [.delete()](#delete)
* [.deleteById()](#deleteById)
* [.discoverDevices()](#discoverDevices)
* [.find()](#find)
* [.get()](#get)
* [.getById()](#getById)
* [.groupBy()](#groupBy)
* [.groupDevices()](#groupDevices)
* [.set()](#set)
* [.setById()](#setById)

<a name="at">
####netbeast(`topic`).at(`location`).METHOD

This method allows us to select a group of devices form a specific location. It can´t be used alone and should be follow by other method.

````javascript
netbeast('lights').at('bedroom').get()
.then(function (data) {})
.catch(function (error) {})
````


In this example, we get information about all the lights placed at the kitchen.

<a name="create">
####netbeast(`topic`).create(`args`)

Create method is used to register a device on the resource on the database. Useful for [creating plugins](../creating_a_plugin). Argument should be a JSON object which contain the name of the app, and the hook to talk to the device.

````javascript
var args = {app: 'flower-power', hook: '/temperature/10.162.63.114'}
netbeast('temperature').create(args)
.then(function (data) {})
.catch(function (error) {})
````

The topic is always required on this method.

<a name="delete">
####netbeast(`topic`).delete(`args`)

The delete method allow us to remove resources from the database. You can use an argument (args: json object) for this method that select an specific property of devices.

````javascript
// Remove all the lights
netbeast('lights').delete()
.then(function (data) {})
.catch(function (error) {})

// Remove all the belkin-wemo lights group by 'colorful'
var args = { app: 'belkin-wemo'}

netbeast('lights').groupBy('colorful').delete(args)
.then(function (data) {})
.catch(function (error) {})
````
<a name="deleteById">
####netbeast(`topic`).deleteById(`id`)

The deleteById method allows us to remove resources from the database. With the id argument we select a specific device from the db.

````javascript
netbeast().deleteById(1)
.then(function (data) {})
.catch(function (error) {})
````

The topic is useless on this method.

<a name="discoveryDevices">
#### netbeast().discoverDevices(`app-name`)

This function allows us to activate the discovery process. With the `app-name` parameter you can specify a concrete app (like belkin-wemo, philips-hue). If you don´t include this argument, the discovery will be apply to all available brands.

````javascript

netbeast().discoveryDevices('sonos')
.then(function (data) {})
.catch(function (error) {})
````
It methods update the database and return an JSON object containing the found devices.

<a name="find">
#### netbeast().find()

This function is useful to know where the Netbeast Dashboard is running. It returns the IP address and the port.

````javascript

netbeast().find()
.then(function (data) {}) // data = {adress: IP, port: PORT}
.catch(function (error) {})
````
It methods update the database and return an JSON object containing the found devices.

<a name="get">
####netbeast(`topic`).get(`value`)

The get method allows us to obtain information about the current state of the devices. You can obtain all the data about the state or specify a concrete value.

````javascript
// Returns the state of all lights
netbeast('lights').get()
.then(function (data) {})
.catch(function (error) {})
````
You can ask for a specific parameter. Find all the parameters available [here](./structure.md#arguments)!
````javascript
// Returns the brightness of all the lights
netbeast('lights').get('brightness')
.then(function (data) {})
.catch(function (error) {})
````
 You can only ask for all values you want on the same request by including the parameters in an **array**.
 ````javascript
 // Returns the brightness of all the lights
 netbeast('lights').get(['brightness', 'color'])
 .then(function (data) {})
 .catch(function (error) {})
 ````

<a name="getById">
#### netbeast(`topic`).getById(`id`)

The getById method allows us to get information about the current state of the devices. You will receive all the information of the specified device.

````javascript
netbeast().getById(1)
.then(function (data) {})
.catch(function (error) {})
````

The topic is useless on this method.

<a name="groupBy">
#### netbeast(`topic`).groupBy(`name`).METHOD

This method allows us to select devices form a specific group. It can´t be used alone and should be follow by other method.

````javascript
netbeast('lights').groupBy('roof').set({power: true})
.then(function (data) {})
.catch(function (error) {})
````

In this example, we switch all the lights of the group ‘roof’ on.

<a name="groupDevices">
#### netbeast(`topic`).groupDevices(`name`, `ids`)
This functión allows us to make group of devices. The argument `name` defines de group name. `Ids` will be an array of ids of the devices that should be grouped.

````javascript
var ids = [1,3, 7 }

netbeast().groupDevices('roof', ids)
.then(function (data) {})
.catch(function (error) {})
````


<a name="set">
#### netbeast(`topic`).set(`args`)

The set method allows us to change the current state of the devices. You can modify different values at the same time.

````javascript
// Change the color of all lights
netbeast('lights').set({color: '#52ff3c'})
.then(function (data) {})
.catch(function (error) {})

//  Change the brightness and color of all the lights
var netbeast = require('netbeast')

netbeast('lights').set({brightness: 80, hue: 350, saturation: 100})
.then(function (data) {})
.catch(function (error) {})
````
<a name="setById">
####netbeast(`topic`).setById(`id`, `args`)

The setById method allows us to change the current state of the given device. You can modify different values of the specified device.

````javascript
var args = { power: true, brightness: 50 }

netbeast().setById(1, args)
.then(function (data) {})
.catch(function (error) {})
````

The topic is useless on this method.
