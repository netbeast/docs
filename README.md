![Netbeast](https://github.com/netbeast-co/router/blob/master/img/full-logo.png?raw=true)

**Netbeast** is an operative system that allows you to control different smart devices under a common control system favouring the communication between them regardless of their brand, the technology they use or how they work. 

Join de community if you want to know more about the project! Visit [Netbeast](http://bit.ly/1FfOLZS)

Also, go to **Downloads** and **Developer** sections and put your developments skills to test!

## Downloads

In order to start developing applications or just trying our system, we propose:

### Raspberry Pi Distributions. 

This is an Operative system based on Linux Distribution for RPI. You can install this operative system to your raspberry pi and you will have our **Netbeast Dashboard** running on your RPI ready to control all your smart home devices. If you want to know how to get it or you want to know more about this project, go here:

[RPI STARTED GUIDE]

Under Development

### Dashboard

**Prerequisites**

You need to install: 
- [nodejs](https://nodejs.org/en/download/) 

If you are running on linux based system just:
```
sudo apt-get install nodejs
```
- npm

Once you install Nodejs, npm is included. 

**Install Netbeast Dashboard**

You can install our dashboard in your pc, and try how it looks. Open your terminal and run:

```
sudo npm install -g nb-dashboard
```

If no erro appears, you will have installed the **Netbeast Dashboard** successfully. Now, let's see how it looks like. Open a terminal and run:
```
nb-dashboard --port 3000
```

Then open your browser and type:
```
localhost:3000
```

And you will see the **Netbeast Dashboard** running on your pc. 

[IMAGEN]

If you want to see how to install an example application, go to our [WIKI](https://github.com/netbeast-co/docs/wiki) or just go to **Develope**r secction

##Developer

As developer, you can access to our full project documentation [WIKI](https://github.com/netbeast-co/docs/wiki)

You can also join the **Netbeast community** [Netbeast](http://bit.ly/1FfOLZS)

###Install an Example application

If you haven't installed the **Netbeast Dashboard** yet, go to **Install Netbeast Dashboard** secction and go for it. 

In other case, we will show you how to install an application and run it in the dashboard

- First one, download an example application.
You can do this running on a terminal

```
npm install -g netbeast
netbeast new app
netbeast package app
```

A new folder named "app" and a folder named "app.tar.gz" will appear. 

Now run the dashboard on the terminal
```
nb-dashboard
```
Open your browser and type:
```
localhost:3000
```
And finally just, drag and drop the folder "app.tar.gz" to the dashboard like this:

[IMAGEN]

Then, you will have installed your app succesfully. Now run it going to this, 

[IMAGEN]

And you will see our "Netbeast Hello World" APP.


## Wiki

Go our wiki site [WIKI](https://github.com/netbeast-co/docs/wiki) where we publish all new features about the project.

## Report an issue or ask us

* [Gitter](http://bit.ly/1dQmFKt)
* [Issues Project](https://github.com/netbeast-co/docs/issues)
* staff@netbeast.co

## Netbeast Roadmap
- Beta (November 9th)
 - [x] Philips Hue Support
 - [x] Wemo Lights Support
 - [x] Wemo Plug Support
 - [ ] Lifx Support
 - [ ] Lockitron Support
 - [ ] Raspberry Pi 2 OS
 - [ ] API Release
 - [ ] Dashboard Re-Desing 
- Beta 2 (November 23rd)
 - [ ] Cloud Service (thethings.io)
 - [ ] Raspberry Pi B Support
 - [ ] Raspberry Pi B+ Support
 - [ ] Tunneling
 - [ ] ...
 - [ ] ...
 
- To be continued...
 

<br/>
<img src="https://github.com/netbeast-co/router/blob/master/img/open-source.png?raw=true" height="140px" width="auto"/><img src="https://github.com/netbeast-co/router/blob/master/img/open-hw.png?raw=true" height="140px" width="auto"/>
