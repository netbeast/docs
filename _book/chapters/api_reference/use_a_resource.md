# Use Netbeast IoT resources

No matter what brand or product you have in your smart house, this is possible with Netbeast:

```javascript
var netbeast = require('netbeast')
netbeast('lights').set({ power: 'on', color: 'red' })
netbeast('music').play('url track').then(function () {
    netbeast.success('Song is being played now')
})
netbeast('shutters').set({ open: 0.5 }) // turn blinds half closed
```