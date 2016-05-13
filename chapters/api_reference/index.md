# API Reference

Welcome to the Netbeast API Documentation!

The main goal of this documentation is to explain how the Netbeast API works. All the information that you need to start building your Apps has been gathered here.

<div class="alert alert-danger">
  Experimental, will probably change
</div>

## How to use it?

First of all, you need to install the npm package in your netbeast app
````
npm install netbeast --save
````
 Once the package is in the node_modules folder, you can require it from the code.

```javascript
var beast = require('netbeast')

beast.find().then(function () {
  beast('lights').get()

  beast('music').at('living-room').set({status: 'play', volume: 100})

  beast('video').get('status')  
})
```

Control your smart devices with Netbeast is as simple as that. Lets go deeper! :rocket:

# IMPORTANT

If you are using the Netbeast API out of our dashboard you will need to declare
in which IP:PORT is the dashboard running.

So, you can do it automatically with:

````javascript

netbeast.find()

````

or manually.

````javascript

netbeast.set({ address: localhost, port: 8000 })

````
