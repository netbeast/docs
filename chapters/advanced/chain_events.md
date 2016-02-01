# Chain events

### Thresholds

```javascript
var netbeast = require('netbeast')
netbeast('temperature').at('garden').when('x < 0')
.then(function() {
    netbeast.warning('Too cold outside')
}
```

There is a limited set of thresholds available in a list.

### _If this then that_

```javascript
var netbeast = require('netbeast')
netbeast('presence').if(function (p) {
    // this function is evaluated everytime presence
    // event happens – if we return true `then` function runs
    return p === 'on'
}).then(function () {
    netbeast.success('Someone came!')
})
```

