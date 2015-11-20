# Node.js wrapper

#About this Docs#

The main goal of this documentation is to explain how the Netbeast API works. All the information that you need to start programmin has been gathered here.

This API is quite new so it is continuously changing and growing. As it matures, some parts are more reliable tan others. Some methods are very new and could be redesigned in the future. Others are so tested and stable. You will see a stability index through all the documentation. We have defined the index as follow:

*   3 - reliable
*   2 - experimental
*   1 - deprecated

##Supported devides##

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

##How to use it?##

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
var resources = require('netbeast/resources')
var scene = require('netbeast/scene')
var devices = require('netbeast/devices')

resources('lights').get()
````

##Resources##

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
