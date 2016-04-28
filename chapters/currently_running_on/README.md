# Currently running on

Netbeast can run on any device that can run Node.js. That being said, there are some requirements that should be met for optimal performance:

* The device should have a min storage of 4GB.
* The device should have a min RAM memory of 1GB for good performance.

## Netbeast on Github

Netbeast is available on its main github repository [here](https://github.com/netbeast/dashboard)

## Netbeast as Desktop App

Netbeast has been adapted to be compiled as desktop application with electron. 
You can see the project repository [here](https://github.com/netbeast/dashboard/tree/electron)

There you will find all the necessary information and steps to compile the code according to you operative system.

- Don't forget to install github to have the best user experience.


It has been tested and compiled on: 

- Linux: 32 & 64 bits
- Mac OSX
- Windows: 32&64 bits

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

## Netbeast on Hardware kits

Netbeast has been successfully tested on the following hardware kits:

1. Raspberry Pi 2
2. Raspberry Pi 3
3. Orange Pi

