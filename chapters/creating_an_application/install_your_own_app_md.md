# Install your own app

If you have not created your app skeleton yet type:

```
netbeast new myapp
```

Apps installed on Netbeast must have a main executable file, run:

```
cd myapp;
chmod +x index.js;
```

Check it has a <u>shebang</u>. After typing `cat index.js` the first line should look like:
```
#!/usr/bin/env node
```

#### Package your app
```
beast pkg .
# alias for "netbeast package"
```

Will output app.tar.gz

**But you could do that also manually!** Using the UNIX compressing tool:
```
tar -zcvf app.tar.gz directory-name
```
Or a standard desktop compressor.

#### Manual installation
Drag and drop the above resulting file to the dashboard, or go to the 'install' section from the tool bar and follow the instructions.

#### Install through SDK
```
beast install app.tar.gz
```
It will prompt to ask you which Netbeast to install in if there are a number of them running in the same network.
