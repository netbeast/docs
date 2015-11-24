#Node.js wrapper#

##About this Docs##

The main goal of this documentation is to explain how the Netbeast API works. All the information that you need to start programming has been gathered here.

This API is quite new so it is continuously changing and growing. As it matures, some parts are more reliable tan others. Some methods are very new and could be redesigned in the future. Others are so tested and stable. You will see a stability index through all the documentation. We have defined the index as follow:

*   3 - reliable
*   2 - experimental
*   1 - deprecated

###Supported devides###

With this API you can control this devices

-   [x] Philips Hue 
-   [x] Belkin WeMo
    -   [x] Switch
    -   [x] Insight
    -   [x] Bulbs
-   [ ] Parrot Flower Power
-   [ ] Chromecast
-   [ ] Sonos
-   [ ] Lifx

###How to use it?###

First of all, you need to install the npm package.
````
sudo npm install netbeast -g
````
 Once the package is in the node_modules folder, you can require it from the code. You are able to require all the methods or only some specific areas.

````javascript
//  Option 1
var nb = require('netbeast')

nb.resources('lights').get()

//  Option 2
var resources = require('netbeast/lib/resources')
var scene = require('netbeast/lib/scene')
var devices = require('netbeast/lib/devices')

resources('lights').get()
````

##Methods##

###Arguments###

Each device can support specific parameters. 
Bridge or Switch can be switched on or off. If you try to set an unsupported parameter to a switch (example, .set({bri: 255})) you will return a soft error. The process keep working but send you a warning.

Here is a list of supported arguments for each device.
*   switch & bridge
    * on - true/false
*   Bulbs
    * on    - true/false
    * bri   - 0-255
    * hue   - 0-65535   (color bulbs)
    * sat   - 0-255     (color bulbs)

A example of use:
````javascript
nb.resources('lights').set({on: true, bri: 200, hue: 0, sat: 255})
````
 If you have white and color bulbs, the first ones are going to switch on and change the brightness. The color bulbs will also change their color to red and the execution continues without problems.


###Output###

All the methods act as a promise and they always return a json object like this:
`````json
{
    error:  
    data:
}
````

###Resources###

A resource contain information about every smart device connected through the dashboard. It has the following fields:

Property    |  Description  |   Values  |   Default
------------|---------------|-----------|----------
id          | Identifies the resource in the db | Integer (automatic) | -
app         | show the device brand | String (belkin-wemo, philips-hue) | -
location    | Location of the devices in the house | String (up to developer) | none
topic       | Define the device field of actuation | String (lights.bridge,switch) | -
group       | Resources con be grouped | String (up to developer) | none

Resources has methods for:
*   Obtain the current state of devices, for expample
````javascript
resources('lights').get()
````
*   Change the current state of devices, for example
````javascript
resources('switch').set({on: true})
````
*   Select a device through its group or location, for example
````javascript
resources('lights').at('kitchen').get('bri')
````

#####resources([topic]).at(location).METHOD#####

This method allows us to select a group of devices form a specific location. It can´t be used alone and should be follow by other method.

````javascript
var nb = require('netbeast')

nb.resources('lights').at('bedroom').get()
.then(function (data) {}
.catch(function (error) {}
````


In this example, we get information about all the lights placed at the kitchen. 

####resources([topic]).delete([args])####

The delete method allow us to remove resources from the database. The args argument is json object with more properties of the device that should be deleted.

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

####resources([topic]).deleteById(id)####

The deleteById method allows us to remove resources from the database. With the id argument we select a specific device from the db.

````javascript
var nb = require('netbeast')

nb.resources().delete(1)
.then(function (data) {}
.catch(function (error) {}
````

The topic is useless on this method.

####resources([topic]).get([value])####

The get method allows us to obtain information about the current state of the devices. You can obtain all the data about the state or specify a concrete value.

````javascript
var nb = require('netbeast')

// Returns the state of all lights
nb.resources('lights').get()
.then(function (data) {}
.catch(function (error) {}

// Returns the brightness of all the lights
var nb = require('netbeast')

nb.resources('lights').get('bri')
.then(function (data) {}
.catch(function (error) {}
````
 You can only ask for one value.  nb.resources('lights').get('on', 'bri') is not allowed.

####resources([topic]).getById(id)####

The getById method allows us to get information about the current state of the devices. You will receive all the information of the specified device.

````javascript
var nb = require('netbeast')

nb.resources().getById(1)
.then(function (data) {}
.catch(function (error) {}
````

The topic is useless on this method.

####resources([topic]).groupBy(name).METHOD####

This method allows us to select devices form a specific group. It can´t be used alone and should be follow by other method.

````javascript
var nb = require('netbeast')

nb.resources('lights').groupBy('roof').set({on: 1})
.then(function (data) {}
.catch(function (error) {}
````

In this example, we switch all the lights of the group ‘roof’ on. 

####resources([topic]).set(args)####

The set method allows us to change the current state of the devices. You can modify different values at the same time.

````javascript
var nb = require('netbeast')

// Change the brightness of all lights
nb.resources('lights').set({bri: 255})
.then(function (data) {}
.catch(function (error) {}

//  Change the brightness and color of all the lights
var nb = require('netbeast')

nb.resources('lights').set({bri: 200, hue: 65000, sat: 255})
.then(function (data) {}
.catch(function (error) {}
````

####resources([topic]). setById(id, args)####

The setById method allows us to change the current state of the given device. You can modify different values of the specified device.

````javascript
var nb = require('netbeast')

var args = { on: 1, bri: 50 }

nb.resources().setById(1, args)
.then(function (data) {}
.catch(function (error) {}
````

The topic is useless on this method.

###Scenes###

A Scene is a snapshot of the current state of a group of devices. It allows you to save your favorites configuration to be accessed easily. The scenes database its composed by the following fields:

Property | Description | Values | Default
---------|-------------|--------|--------
id | Identifies the resource in the db | Integer (automatic) | -
sceneid | show the name of the scene | String | -
location | Location of the scene in the house | String (up to developer) | none
on | show if the device is on or off | Boolean	| -
bri	| Stores the brightness value | Integer |	-
hue	| Stores the hue value | Integer | -
sat	| Stores the saturation value | Integer | -

A given device could be part of different scenes.

The parameters *hue* and *sat* are used to define the colors.

####scene(sceneid).addDevice(id)####

The addDevice method allows us to add a new device to the selected scene. You must pass the id of the device and it will save the current state of it on the db.

````javascript
var nb = require('netbeast')

nb.scene('watchfilm').addDevice(2)
.then(function (data) {}
.catch(function (error) {}
````

####scene(sceneid).apply()####

This method apply the configuration of the given scene.

````javascript
var nb = require('netbeast')

nb.scene('watchfilm').apply()
.then(function (data) {}
.catch(function (error) {}
````

####scene(sceneid).create(ids)####

This method is used to create a new scene by passing an array of device ids. It takes the current state of the given devices and store the scene in the db with the 'seceneid' name.

````javascript
var nb = require('netbeast')

var devices = [1, 2, 6, 9]

nb.scene('watchfilm').create(devices)
.then(function (data) {}
.catch(function (error) {}
````

####scene(sceneid).createCustom(state)####

With this method you can create a new scene with a predefined state. *state* is an object array that contains the object id and the state of each device.

````javascript
var nb = require('netbeast')

var newscene = [ { 
    id: 1,
    on: 1,
    bri: 254,
    hue: 4753,
    sat: 254 },
    {
    id: 8,
    on: 1,
    bri: 254}]


nb.scene('watchfilm').createCustom(newscene)
.then(function (data) {}
.catch(function (error) {}
````

####scene(sceneid).delete()####

With delete you can remove a given scene from the db

````javascript
var nb = require('netbeast')

nb.scene('watchfilm').delete()
.then(function (data) {}
.catch(function (error) {}
````

####scene(sceneid).deleteDevice(id)####

Instead of removing the whole scene, you are able to quit one device from the scene.

````javascript
var nb = require('netbeast')

nb.scene('watchfilm').deleteDevice(6)
.then(function (data) {}
.catch(function (error) {}
````


####scene(sceneid).get()####

This methods returns all the information about the scene.

````javascript
var nb = require('netbeast')

nb.scene('watchfilm').get()
.then(function (data) {}
.catch(function (error) {}
````
get has no arguments.

####scene().getScenes()####

The getScenes method return the name of all the scenes registered on the db.
Arguments are not needed on this function.

````javascript
var nb = require('netbeast')

nb.scene().getScene()
.then(function (data) {}
.catch(function (error) {}
````


###Devices###
This object include useful methods for managing different aspects of the Smart devices

####devices.group(name , devicesId)####
This functión allows us to make group of devices. The argument name defines de group name. DevicesId will be an array of ids of the devices that should be grouped.

````javascript
var nb = require('netbeast')

var args = [1,3, 7 }

nb.devices().group('roof', args)
.then(function (data) {}
.catch(function (error) {}
````

####devices.discover([brand-name])####

This function allows us to activate the discovery process. With the brand-name parameter you can specify a concrete app (like belkin-wemo, philips-hue). If you don´t include this argument, the discovery will be apply to all available brands.

````javascript
var nb = require('netbeast')

nb.devices().discovery('belkin-wemo')
.then(function (data) {}
.catch(function (error) {}
````
