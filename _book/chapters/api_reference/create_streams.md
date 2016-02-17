# Create streams

Streams are created manually through a plugin. When ready we just declare them as usual. With a little variation.

Streams can be _sinks_ a.k.a. _consumers_ or _feeds_ a.k.a. _providers_: 
* A sink is somewhere to push the video to, where is consumed: chromecast, for example.
* A feed is some stream that can be sent to a sink, that is produced e.g: a security camera.

```javascript
var netbeast = require('netbeast')
var resource = netbeast('video')
.create({location: 'baby room', stream: 'feed'})
.then(function () {
    netbeast.info('Video feed available')
})
.catch(function () {
    netbeast.error('something went wrong')
})
```

Stream can be `feed|sink`. If you are in the very rare case of a bidirectional product that accepts and sends video at the same time, just open two resourcers.