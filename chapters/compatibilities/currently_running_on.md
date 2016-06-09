# Currently running on

Netbeast can run on any device that can run Node.js. That being said, there are some requirements that should be met for optimal performance:

* The device should have a min storage of 4GB.
* The device should have a min RAM memory of 1GB for good performance.

## Netbeast on Hardware kits

Netbeast has been successfully tested on the following hardware kits:

1. Raspberry Pi 2 - Raspbian Jessie
2. Raspberry Pi 3 - Raspbian Jessie Lite
3. Orange Pi - Raspbian Jessie
4. Pine64 - ArchLinux 64 bits

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

## Netbeast on Open-WRT

We have compiled Netbeast for Open-WRT. The only thing you need to do is compile Nodejs on it, see [this](https://netbeast.co/blog/how-to-cross-compile-nodejs-for-openwrt) and install Netbeast in any of this ways.

