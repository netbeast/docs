# Create your first plugin :wrench:

A plugin is a Netbeast app that people to control hardware that has not yet been
ported to the API or that has been invented by you, a maker.

<iframe src="http://netbeast.github.io/bulb-plugin/" frameBorder="0" width="100%" height="400px"></iframe>

### Create the app skeleton:
Let's use the sdk to make things faster and try it live.
Click [here](../get_started/install_dashboard.md) if you have not installed it yet.

```
beast new bulb-plugin; cd bulb-plugin
npm install
```

Open the **bulb-plugin** folder with your favorite editor or IDE.
You should have now a file structure like this:
```
.
├── LICENSE
├── README.md
├── node_modules
│   ├── express
│   ├── minimist
│   └── netbeast
├── package.json
├── public
│   └── index.html
└── server.js
```

Now let's get started. Declare your app as a plugin. Append the following lines to **package.json** before the closing `}` tag.
```
  "netbeast": {
    "type": "plugin"
  }
```

## The hardware: a hacked example
We are going to **mimic hardware** connection by creating a really simple webapp. For the result below you must copy paste the following code for a new **index.html**:

### index.html
```html
<head>
  <title>Netbeast Bulb Plugin</title>
  <link rel="stylesheet" href="bulb.css" media="screen" charset="utf-8">
  <link rel="stylesheet" href="style.css" media="screen" charset="utf-8">
</head>

<body>
  <div class="top-decoration"></div>
  <div id="plugin front-end">
  </div>
  <div class="bulb-container small">
    <div class="bulb light">
      <div id="bulb">
        <div class="bulb top"></div>
        <div class="bulb middle-1"></div>
        <div class="bulb middle-2"></div>
        <div class="bulb middle-3"></div>
        <div class="bulb bottom"></div>
      </div>
      <div id="base">
        <div class="screw-top"></div>
        <div class="screw a"></div>
        <div class="screw b"></div>
        <div class="screw a"></div>
        <div class="screw b"></div>
        <div class="screw a"></div>
        <div class="screw b"></div>
        <div class="screw c"></div>
        <div class="screw d"></div>
      </div>
    </div>
  </div>
    <div class="code-container">
      <pre><i class="txt-red">beast</i>(<i class="txt-green">'lights'</i>).<i class="txt-blue">set</i>({
  <i class="txt-green">color</i>: <i class="txt-green">"<input id="color" type="text" class="color" name="color" value="00fea5">"</i>,
  <i class="txt-green">power</i>: <i class="txt-green">"<input id="power" type="text" class="power" name="power" value="on">"</i>
})</pre>
    <div id="run-btn">
      RUN
    </div>
  </div><!-- wrapper -->

  <!-- declares bulb features and methods -->
  <script type="text/javascript" src="bulb.js"></script>
  <!-- real time comms library -->
  <script type="text/javascript" src="socket.io"></script>
  <!-- simulates hardware communication -->
  <script type="text/javascript" src="hw-api.js"></script>
</body>
```

### bulb.js
This is what the physical hardware is exptected to do: behave like a bulb.
So it is just a set of listeners and animations:

```javascript
var color = document.getElementById('color')
var power = document.getElementById('power')
var bulb = document.getElementById('bulb')
var button = document.getElementById('run-btn')
var light = document.getElementById('light')

button.onclick = function toggleBulbState () {
  changeBulbParams({ color: color.value, power: power.value })
}

function setBulbParams (params) {
  if (params.power === 'off') {
    params = { color: 'E7E7E7' }
  }
  console.log('set params', params)

  var bulb_parts = ['.bulb.middle-1', '.bulb.middle-2', '.bulb.middle-3']

  document.querySelector('.bulb.top').style.boxShadow = '0px 0px 98px #' + params.color

  document.querySelector('.bulb.top').style.backgroundColor = params.color
  document.querySelector('.bulb.bottom').style.backgroundColor = params.color
  bulb_parts.forEach(function (className) {
    document.querySelector(className).style.borderTopColor = params.color
  })
}

function changeBulbParams (params) {
  console.log('change params', params)
  /* Overwrite html fields if necessary */
  color.value = params.color || color.value
  power.value = params.power || power.value
  setBulbParams({color: color.value, power: power.value})
}
```

### hw-api.js
This is the actual mimic of the hardware interface. It pretends to be a bulb controlled through websockets. Check it out:
```javascript
var socket = io.connect({path: '/i/bulb-plugin'})

socket.on('connect', function () {
  console.log('ws:// bulb is online')
})

socket.on('disconnect', function () {
  console.log('ws:// connection with bulb lost')
})

socket.on('set', function (params) {
  changeBulbParams(params)
})

socket.on('on', function () {
  if (bulbState === 'off') {
    bulb.onclick()
  }
})

socket.on('off', function () {
  if (bulbState === 'on') {
    bulb.onclick()
  }
})

socket.on('get', function () {
  socket.emit('params', {
    power: bulbState,
    brightness: brightness.value,
    color: color.value
  })
})
```

### The plugin code
For your code to be available for the Netbeast API you must implement HTTP routes.
This we'll make your IoT plugin available for the rest of apps installed in the
Netbeast and so for any other developer.

```javascript
var express = require('express')
var request = require('superagent')

var router = express.Router()
var bulbParams // aux nasty way to transmit changes

module.exports = function (io) {
  io = io

  io.on('connection', function () {
    console.log('ws:// bulb has connected to plugin')
  })

  io.on('disconnection', function () {
    console.log('ws:// bulb has disconnected from plugin')
  })

  io.on('connect_failure', function (err) {
    console.log('ws:// connection failure')
    console.log(err)
  })

  request.post(process.env.LOCAL_URL + '/api/resources')
  .send({ app: 'bulb-plugin', topic: 'lights', hook: '/api' })
  .end(function (err, resp) {
    if (err) return console.log(err)
    console.log(resp.text)
    console.log(resp.body)
  })

  router.post('/', function (req, res) {
    console.log('Plugin translates uniform req.body to bulb params...')
    console.log(req.body)
    io.emit('set', {
      brightness: req.body.bri,
      color: req.body.hue,
    })
    console.log('setting...')
    console.log({
      brightness: req.body.bri,
      color: req.body.hue,
    })
    if (req.body.on) io.emit('on')
    if (req.body.off) io.emit('off')
    if (req.body.power) io.emit(req.body.power)
    res.status(204).end()
  })

  router.get('/', function (req, res) {
    io.emit('get')
    var timerReference = setTimeout(function () {
      if (bulbParams) {
        res.json(bulbParams)
      } else {
        res.status(200).json({ error: 'No bulb available' })
      }
    }, 3000)
  })

  router.get('/on', function (req, res) {
    io.emit('on')
    res.status(204).end()
  })

  router.get('/off', function (req, res) {
    io.emit('off')
    res.status(204).end()
  })

  return router
}
```

This virtual IoT device implements a HTTP (non restful) api with the following methods `GET` (on, off, status) and `POST` color, power.

But for all developers to reuse those methods through Netbeast API you must declare
those hook them as available on _light_ topic.

#### With `require('netbeast')`
```javascript
var options = { hook: '/api' } // base route for your HTTP API '/' by default
netbeast('lights').create(options).then(...)
```

#### With Netbeast router HTTP RESTful API
```javascript
// As is present in the above plugin.js file
request.post(process.env.LOCAL_URL + '/api/resources')
  .send({ app: 'bulb-plugin', topic: 'lights', hook: '/api' })
  .end(function (err, resp) {
    if (err) return console.log(err)
  })
```
