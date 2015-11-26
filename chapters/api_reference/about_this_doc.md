# About this doc

The main goal of this documentation is to explain how the Netbeast API works. All the information that you need to start programming has been gathered here.

This API is quite new so it is continuously changing and growing. As it matures, some parts are more reliable tan others. Some methods are very new and could be redesigned in the future. Others are so tested and stable. You will see a stability index through all the documentation. We have defined the stability index as follow:

*   3 - reliable
*   2 - experimental
*   1 - deprecated

## Supported devices

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
-   ...

## How to use it?

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