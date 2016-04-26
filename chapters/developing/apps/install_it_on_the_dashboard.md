# Installing Netbeast applications

Once you have created your first app, you will be able to install it on Netbeast. There are some ways to do so:

## Installing applications through Explore

You can publish your apps on our Github repository and make them publicly available through the `Explore`section. More info on that here.

To install apps through `Explore`, click on the `explore` icon and look for the app that you want to install.

## Installing through github

We previously installed the padjs app through this method.

1. First, you need to upload your application to a github repository. 
2. Then, go to the `Install` section on the Dashboard and then click on the option "with git".
3. Finally, copy your repository URL  and click on `install`.

## Installing through drag & drop

First you need to package your folder application in a .tar.gz format, we **recommend** you to do that with the Toolbelt. 

Run on your apps' folder:

```
netbeast pkg .
```

It will output app.tar.gz.


*Alternatives*

You can also use the UNIX compressing tool:
```
tar -zcvf app.tar.gz directory-name
```
Or a standard desktop compressor.

Finally, go to the `install` section in the dashboard and drag your packaged app onto the dragable area.

## Installing through the Toolbelt

Assuming you've already packaged your app into a tar.gz file, run:
```
netbeast install app.tar.gz
```

If you have two or more devices running Netbeast on the network, it will ask you on which Netbeast to install.