# Currently running on

Netbeast can run on any device that can run Node.js. That being said, there are some requirements that should be met for optimal performance:

* The device should have a min storage of 4GB.
* The device should have a min RAM memory of 1GB for good performance.

## Netbeast on Github

Netbeast is available on its main github repository [here](https://github.com/netbeast/dashboard)

## Netbeast on NPM

Netbeast is available on NPM repository [here](https://www.npmjs.com/package/netbeast-cli). You can install it easily as follows:

```
npm install -g netbeast-cli
```

## Netbeast on Docker

Netbeast has its own docker image available [here](https://hub.docker.com/r/netbeast/netbeast/). Now let's see how you can run the docker image.

First you need to install docker. Click [here](https://docs.docker.com/engine/installation/) to see how


Once we have all set up, start a docker terminal and see what is the **IP assigned** to that container

Download the netbeast image from dockerhub

```
docker pull netbeast/netbeast
```

Run it

```
docker run -p 49160:8000 -d netbeast/netbeast
```

This will run your docker container on the port 49160

4.Play with it

Now access to the docker container url

>http://IP_assigned:49160

## Netbeast on Node-Red

Node-RED is a tool for wiring together hardware devices, APIs and online services in new and interesting ways.

Netbeast has been uploaded as a flow for node-red. Look [here](http://flows.nodered.org/node/node-red-contrib-netbeast)

You can check [this](https://www.toptal.com/nodejs/programming-visually-with-node-red) interesting post about how to start using Netbeast with Node-Red

## Netbeast as Desktop App

Netbeast has been adapted to be compiled as desktop application with electron. 
You can see the project repository [here](https://github.com/netbeast/dashboard/tree/electron)

There you will find all the necessary information and steps to compile the code according to you operative system.

- Don't forget to install github to have the best user experience.


It has been tested and compiled on: 

- Linux: 32 & 64 bits
- Mac OSX
- Windows: 32&64 bits

## Netbeast on Open-WRT

We have compiled Netbeast for Open-WRT. The only thing you need to do is compile Nodejs on it, see [this](https://netbeast.co/blog/how-to-cross-compile-nodejs-for-openwrt) and install Netbeast in any of this ways.

## Netbeast on Hardware kits

Netbeast has been successfully tested on the following hardware kits:

1. Raspberry Pi 2 - Raspbian Jessie
2. Raspberry Pi 3 - Raspbian Jessie Lite
3. Orange Pi - Raspbian Jessie
4. Pine64 - ArchLinux 64 bits

