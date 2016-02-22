# API Reference

Welcome to the Netbeast API Documentation!

The main goal of this documentation is to explain how the Netbeast API works. All the information that you need to start building your Apps has been gathered here.

## How to use it?

First of all, you need to install the npm package in your netbeast app
````
npm install netbeast --save
````
 Once the package is in the node_modules folder, you can require it from the code.

```javascript
var beast = require('netbeast')

beast('lights').get()

beast('music').at('living-room').set({status: 'play', volume: 100})

beast('video').get('status')
```

Control your smart devices with Netbeast is as simple as that. Lets go deeper! :rocket:
