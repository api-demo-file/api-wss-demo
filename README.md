### NodeJS
``` NodeJS
const pako = require('pako')

const WebSocket = require('ws')

const ws = new WebSocket('wss://ws.ahighapi.com/wss')

ws.on('open', function open() {
  // 发送订阅的数据
  // dataType 1 表示订阅压缩的数据
  var json = {
    "data": {
      "type": "market",
      "dataType": 1,
    },
    "action": "Topic.sub"
  }
  var data = JSON.stringify(json);
  ws.send(data);
})

ws.on('message', function (data) {
  var rs = pako.inflate(data, { to: 'string' })
  console.log(rs);
})
```



### PHP
``` PHP
function decodeWss($msg)
{
  return json_decode(gzdecode($msg),true);
}
```
