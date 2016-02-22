# Structure Overview

Netbeast API is composed by different methods. These groups of methods try to help
you communicating your Apps with the smart devices and Dashboard in an easy way.

* [Methods](#methods)
  * [Arguments](#arguments)
  * [Output](#output)
* [Dashboard Databases](#DD)
  * [Resources db](#resourcesdb)
  * [Scenes db](#scenesdb)

<a name="methods">
#Methods

We can find methods for different purposes:
* [Manage smart devices](./resources.md)
* [Create and use Scenes](./scenes.md)
* [Send notifications to Dashboard](./push_notifications.md)
* [Catch events](./chain_events.md)

<a name="arguments">
###Arguments

Each device support specific parameters.
If you try to set an unsupported parameter to a switch (for example the brightness, `beast('switch').set({brightness: 80})`) you will return a soft error. The process keep working but send you a warning.

Here is a list of supported arguments for each device.
* switch & bridge
    * power:  `true || false`
* lights
    * power:    `true || false`
    * hue:           `0..360`
    * saturation:    `0..100`
    * brightness:    `0..100`
    * color: `{r: 0, g: 0, b: 0} || #FF13AA`
* music & video
    * volume:       `0..100`
    * status:       `play || pause || stop || mute || unmute || info`
    * track:        `must be the url of the song/video`
* temperature       `ºC`
* humidity          `0..100`
* luminosity        `photons per square meter`
* battery           `0..100`

A example of use:
````javascript
var beast = require('netbeast')
beast('lights').set({power: true, brightness: 100, hue: 0, saturation: 100})
````
 If you have white and color bulbs, the first ones are going to switch on and change the brightness. The color bulbs will also change their color to red and the execution continues without problems.

<a name="output">
###Output

All the methods acts as a promise and they always return a Javascript object if successful or an error object else.
````javascript
var beast = require('netbeast')

beast('temperature').at('kitchen').get()
.then(function (data) {
  console.log('The temperature in the kitchen is ' + data + 'ºC')
}).catch(function (err) {
  console.log('Error: ' + err)
})
````

<a name="DD">
## Dashboard Databases

Netbeast Dashboard store 2 different databases that helps on the manage of the
smart devices. In order to make the API easier to understand, we are going to talk
a bit about how these databases are structured.

<a name="resourcesdb">
### Resources
A resource contain information about every smart device connected through the dashboard. It has the following fields:

Property    |  Description  |   Type    |   Example
------------|---------------|-----------|----------
id          | Identifies the resource in the db | Integer (autoincrement) | 1
app         | Name of the app that register the resource | String (belkin-wemo, philips-hue) | sonos
location    | Location of the devices in the house | String (up to developer) | bedroom
topic       | Define the device field of actuation | String (lights, music, switch, video) | music
group       | Resources can be grouped | String (up to developer) |
hook        | Used to communicate with a device and identify it | string | /sonos/{IP} (/sonos/172.64.30.114)

<a name="scenesdb">
### Scenes

A Scene is a snapshot of the current state of a group of devices. It allows you to save your favorites configuration to be accessed easily. The scenes database its composed by the following fields:

Property | Description | Values | Example
---------|-------------|--------|--------
id | Identifies the resource in the db | Integer | 3
scene_id | show the name of the scene | String | cinema
location | Location of the scene in the house | String (up to developer) | living-room
status   | store the state to be applied on the device | String	| '{power: on, brightness: 50}'

A given device could be part of different scenes.
