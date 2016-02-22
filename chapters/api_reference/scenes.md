# Scenes

A Scene is a snapshot of the current state of a group of devices. It allows you to save your favorites configuration to be accessed easily.
A given device could be part of different scenes.

Index:

* [.addDeviceScene()](#addDeviceScene)
* [.applyScene()](#applyScene)
* [.createScene()](#createScene)
* [.createCustomScene()](#createCustomScene)
* [.deleteDeviceScene()](#deleteDeviceScene)
* [.deleteScene()](#deleteScene)
* [.getAllScenes()](#getAllScenes)
* [.getScene()](#getScene)

<a name="addDeviceScene">
####netbeast(`sceneid`).addDeviceScene(`id`)

The addDevice method allows us to add a new device to the selected scene. You must pass the id of the device and it will save the current state of it on the db.

````javascript
netbeast('watchfilm').addDeviceScene(2)
.then(function (data) {})
.catch(function (error) {})
````

<a name="applyScene">
####netbeast(`sceneid`).applyScene()

This method apply the configuration of the given scene.

````javascript
netbeast('watchfilm').applyScene()
.then(function (data) {})
.catch(function (error) {})
````

<a name="createScene">
####netbeast(`sceneid`).createScene(`ids`)

This method is used to create a new scene by passing an array of device ids. It takes the current state of the given devices and store the scene in the db with the 'seceneid' name.

````javascript
var devices = [1, 2, 6, 9]

netbeast('watchfilm').createScene(devices)
.then(function (data) {})
.catch(function (error) {})
````

<a name="createCustomScene">
####netbeast(`sceneid`).createCustomScene(`state`)

With this method you can create a new scene with a predefined state. *state* is an object array that contains the object id and the state of each device.

````javascript
var newscene = [ {
        id: 1,
        status: {
          power: true,
          brightness: 99,
          hue: 200,
          saturation: 80
        }
    },
    {
        id: 8,
        status: {
          volume: 90,
          track: `url-track`,
        }
    }]


netbeast('watchfilm').createCustomScene(newscene)
.then(function (data) {})
.catch(function (error) {})
````

<a name="deleteDeviceScene">
####netbeast(`sceneid`).deleteDeviceScene(`id`)

Instead of removing the whole scene, you are able to quit one device from the scene.

````javascript
netbeast('watchfilm').deleteDeviceScene(6)
.then(function (data) {})
.catch(function (error) {})
````

<a name="deleteScene">
####netbeast(`sceneid`).deleteScene()

With delete you can remove a given scene from the db

````javascript
netbeast('watchfilm').deleteScene()
.then(function (data) {})
.catch(function (error) {})
````

<a name="getAllScenes">
####netbeast().getAllScenes()

The getScenes method return the name of all the scenes registered on the db.
Arguments are not needed on this function.

````javascript
netbeast().getAllScenes()
.then(function (data) {})
.catch(function (error) {})
````

<a name="getScene">
####netbeast(`sceneid`).getScene()

This methods returns all the information about the scene.

````javascript
netbeast('watchfilm').getScene()
.then(function (data) {})
.catch(function (error) {})
````
getScene has no arguments.
