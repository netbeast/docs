# How to use it?

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