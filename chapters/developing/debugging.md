# Debugging
 Netbeast Dashboard clones or downloads apps to a `.sandbox` folder relative to its root. Move apps there for them to be listed on *installed apps* or *installed plugins*.


#### Restart the app
 Sometimes you have to stop your app and tell node to run the new source. You can achieve it with tools like [nodemon](http://nodemon.io/). If you want the Dashboard to relaunch it (e.g: you are using Netbeast API and need environment variables) run: 
```bash
beast restart <your app name>
```
 