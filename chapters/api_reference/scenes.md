# Scenes

A Scene is a snapshot of the current state of a group of devices. It allows you to save your favorites configuration to be accessed easily. The scenes database its composed by the following fields:

Property | Description | Values | Default
---------|-------------|--------|--------
id | Identifies the resource in the db | Integer (automatic) | -
scene_id | show the name of the scene | String | -
location | Location of the scene in the house | String (up to developer) | none
power | show if the device is on or off | String	| -
brightness	| Stores the brightness value | Integer |	-
hue	| Stores the hue value | Integer | -
saturation	| Stores the saturation value | Integer | -

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
        power: 'on',
        brightness: 99,
        hue: 200,
        saturation: 80 
    },
    {
        id: 8,
        power: 'on',
        brightness: 254
    }]


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
