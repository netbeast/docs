# Chain events


### _If this then that_

```javascript
var netbeast = require('netbeast')
netbeast('temperature').on(function (message) {
    // this function is called everytime temperature
    // event happens
    if (message.temperature > 30) {
        // do something
    }
})
```

