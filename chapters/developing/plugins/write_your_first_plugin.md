# Write your first Plugin

A Netbeast plugin is a kind of "application" that allow you to control device from a concrete brand through the [Netbeast API](../../api_reference/index.md)
It's the sauce behind Netbeast API engine. With a plugin you can register a resource
for others to use, like a new brand of smart bulbs to be controlled as another _light_ source.

If you want to control a device that it´s yet not supported by Netbeast. You can **create a plugin
and make it available for all the community**.

Lets connect everything!

In this section we are going to explain how to create a plugin for real products. However, you can still learn and try how to create plugins with Netbeast without any real product on this secction: [Write a virtual plugin](write_a_virtual_plugin.md)

____________________________________________________________________________________________________________

Creating a new plugin with Netbeast is really easy because its simple structure.
With the help of `netbeast-cli` you only need to follow a few steps to have your plugin running.

First we will install the netbeast SDK. Open a terminal and type:
```
npm install -g netbeast-cli
netbeast new myplugin --plugin
```

A new folder named _myplugin_ will contain some code scaffolded.

**A basic Netbeast plugin looks like this:**
```
.
├── src
│   ├── index.js
│   ├── resources.js
│   └── routes.js
├── package.json
├── index.js
├── README.md
└── test.js

```

##package.json
package.json is the information needed by npm to maintain a module into their repositories, analyze dependencies and establish some development workflow.

Netbeast will make use of this file to reduce the overhead of configuration needed to get up and running. It will look for the `main`field in order to launch and executable. For this app:
```json
{
    "name":"myplugin",
    "version": "1.0.0",
    "description":" A short description about what is your plugin for.",
    "main": "index.js",
    "netbeast": {
      "bootOnLoad": true,
      "type": "plugin"
    },
    "dependencies": {
      "async": "^1.4.2",
      "body-parser": "^1.14.0",
      "chai": "^3.2.0",
      "commander": "^2.8.1",
      "express": "^4.13.3",
      "fs": "0.0.2",
      "http": "0.0.0",
      "mocha": "^2.3.2",
      "morgan": "^1.6.1",
      "netbeast": "^1.0.2",
      "request": "^2.62.0",
      "socket.io": "^1.3.7"
    },
    "devDependencies":{},
    "scripts":{
        "test":"node test.js",
        "start": "node index.js"
    },
    "repository": {
        "type":"git",
        "url":"https://github.com/netbeast/docs"
    },
    "keywords": [ "iot","netbeast","netbeast.co", "plugin"],
    "author": "pablo@netbeast.co",
    "license": "GPL 2",
    "bugs": {
        "url":"https://github.com/netbeast/docs/issues"
    },
    "homepage":"https://github.com/netbeast/docs"
}

```

The field `bootOnLoad` allows the plugin to start on boot.

**IMPORTANT**: don´t forget to fill `type`as plugin.

## index.js & src/index.js

This files implements a simple HTTP server. It´s already configured to work with
Netbeast dashboard, so you won't need to modify it.

**It is mandatory for `main` to be and executable file.** So make sure it can be executed:
```
chmod +x index.js
```
As you can see in the code, **the runnable must accept the port by parameter**, so they can all be opened from the [Dashboard](https://github.com/netbeast/dashboard).

## src/resources.js

We use this file to discover the devices.
Once we find a device, we shuold:
  1. Register the device in the database, by following the given structure
  2. If the device is not available anymore, we should delete it from the database

```javascript
var request = require('request')
var netbeast = require('netbeast')

module.exports = function (callback) {
  // First we ask the database for all the devices of the same brand that are stored
  // We stored the hooks of this devices in the 'objects' array
  var objects = []

  // Request to the database
  netbeast().get({app: NAME_PLUGIN})
  .then(function (data) {
    if (!data) return callback()

    // Store the found devices in 'objects' array
    if (data.length > 0) {
      data.forEach(function (device) {
        if (objects.indexOf(device.hook) < 0) objects.push(device.hook)
      })
    }   
  }).catch(function (err) {return callback(err)})

  // Implement the device discovery method

  // When we find a device
  //  1. Look if its already exists on the database.
  var indx = objects.indexOf('/HOOK/id') // hook == /Namebrand/id. Example. /hueLights, /Sonos
  // We will use the id to access to the device and modify it.
  // Any value to refer this device (MacAddress, for example) can work as id

  //  2. If the hook is in 'objects' array, delete it from the array
  if (indx >= 0) {
    objects.splice(indx, 1)

  // 3. If this device is not registered on the database, you should register it
  } else {
    //  Use this block to register the found device on the netbeast database
    //  in order to using it later
    netbeast('TOPIC').create({app: 'NAME_PLUGIN', hook: '/HOOK/id'})
    .cathch(function (err) {
      return callback(err)
    })
            // NAME_PLUGIN = Name of the plugin
            // TOPIC = lights, bridge, switch, temperature, music, etc
            // HOOK == /Namebrand  Example. /hueLights, /Sonos
      // We will use the id to access to the device and modify it.
      // Any value to refer this device (MacAddress, for example) can work as id
      // netbeast('lights').create({app: 'philips-hue', hook: /hueLights/172.64.27.114})
  }

  // If there exists 'hooks' stored on the 'objects' array, it means that
  // this devices are stored on the databases but are not reachable. We should
  // delete this devices from the database using the code given.
  if (objects.length > 0) {
    objects.forEach(function (hooks) {
      //  Use this block to delete a device from the netbeast database
      netbeast().delete({hook: hooks})
      .catch(function (err) {
        return callback (err)
      })
    })
  }

  /*
  This function is called from route.js, so
  if you need to pass any information to this file you can do it
  by using the callback ( callback(error, devices) , for example)
  */
  return callback(null)
}

```

Each device has different discovery methods. If you still having doubts or don't know
how to proceed, **check the existing plugins** in our [GitHub](http://github.com/netbeast)

## src/routes.js

In this file you will receive the request from Netbeast API. And you should translate
it to the proper methods. We have 3 routes.

```javascript

var express = require('express')
var router = express.Router()
// Require the discovery function
var loadResources = require('./resources')

loadResources(function (err) {
  if (err) return console.log(err)

  router.get('/HOOK/:id', function (req, res, next) {
    ...
  })

  // Used to trigger the discovery method. Should return the new found devices
  router.get('/discover', function (req, res, next) {
    loadResources(function (err) {
      if (err) return res.status(500).send(err)
    })
  })

  router.post('/HOOK/:id', function (req, res, next) {
    ...
  })
})

// Used to serve the routes
module.exports = router
```

Use `get('/HOOK/:id')` to gather info from the device like in this example.
The parameters that you should look for are provided in `req.query`.

```javascript
var colorsys = require('colorsys')
var bulbvalues = {power: 'on', brightness: 'bri', saturation: 'sat', hue: 'hue'}

router.get('/hueLights/:id', function (req, res, next) {
    api.lightStatus(req.params.id, function (err, data) {
      if (err) return res.status(404).send('Device not found')

      if (!Object.keys(req.query).length) return res.json(_parsePhilips(data.state))
      var response = {}
      Object.keys(req.query).forEach(function (key) {
        if (key === 'color') {
          response['color'] = { hex: colorsys.hsl2Hex(data.state.hue, data.state.sat, data.state.bri),
                             rgb: colorsys.hsl2Rgb(data.state.hue, data.state.sat, data.state.bri) }
        }
        if (bulbvalues[key]) response[key] = _parseKeyGet(key, data.state[bulbvalues[key]])
      })
      if (Object.keys(response).length) return res.json(response)
      return res.status(202).send('Values not available on this philips-hue bulb')
    })
  })
```

Use `post('/HOOK/:id')` to change the device status like in this example.
The parameters that you should modify are provided in `req.body`.

```javascript
var ledpanel = require('ledpanel')

router.post('/ledPanel/:id', function (req, res, next) {
  //req.body = {power:on/off, data:[]}
  if (!req.body.power) return res.status(400).send('Incorrect format {power:on/off, data}')

  if (req.body.power === 'off') {
    ledpanel.clear(function(err) {
      if(err) return res.status(400).send('A problem setting one value occurred')
      return res.send({power: req.body.power})
    })
  } else {
    ledpanel.matrix(req.body.matrix, function(err) {
      if(err) return res.status(400).send('A problem setting one value occurred')
      return res.send(req.body)
    })
  }
  return res.status(400).send('Incorrect format {power:on/off, data}')
})
```
If you use `netbeast new myplugin --plugin` to create a plugin, you will find this
info and much more inside. You can find more examples on our [GitHub](http://github.com/netbeast).


## test.js

This file is empty, but is a good practice to develop some test for your plugin.
