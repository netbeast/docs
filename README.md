# About Netbeast

This documentation will show you all there is to know about Internet of Things development with Netbeast. For basic info on what Netbeast is about, please see [the main project website](https://netbeast.co).

Anxious to start right away?

[Get Started](chapters/getting_started/installing_and_cloning.md)

## What is Netbeast?

As our Github reads:

Netbeast is an open source platform that allows to connect IoT devices regardless of anything.

More specifically, Netbeast is:

* A Toolbelt that let's you develop Internet of Things applications easier and faster.
* A platform that hosts your applications and does the hard work of specifically talking to every device.

Logically, it makes sense to combine the use of both to create and offer IoT applications to everyone. Let's have a peek at how it works.


## Hello world

Our "Hello World" IoT version is a small application that turns a light into any color we want.

```
var beast = require('netbeast')

    beast('lights').set({
      color: "#9AD74C",
      power: "on"
    })
```
Here, the application is using:

[The Netbeast API](http://docs.netbeast.co/chapters/api_reference/index.html) to tell a light, any light, to turn on and with a lime green color. 

[The Netbeast Dashboard](chapters/getting_started/dashboard.md) is running on the device where this application is running. This allow to translate messages from any kind of devices.

And that's all there is to it. Using the same principle one can control any device (lights, sound systems, TVs, appliances...).


## Apps & Plugins

That's how you use the API to develop applications. The API itself uses [plugins](http://docs.netbeast.co/chapters/creating_a_plugin/write_your_first_plugin.md) to communicate specifically with each brand's devices. Plugins are modular and specific to a certain vendor API or protocol.


## Dashboard

The dashboard hosts and runs applications. It provides a user interface from which you can access and manage all your applications.


![Demo Dashboard](/img/dashboard-demo.gif)


## About these docs

This documentation is broken down into four parts:
* Getting started does an overview of all the tools available and walks you through the setup process on every available platform.
* Developing teaches you all there is to know about creating applications and plugins for connected products.
* API reference is the place to go to learn everything about the Netbeast API and its methods.
* Contributing provides all the guidelines necessary to submit your code and help improve Netbeast.








