### NodeJS

```javascript

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


### Java

``` java

private static byte[] gzip(String s) throws Exception {
    ByteArrayOutputStream bos = new ByteArrayOutputStream();
    GZIPOutputStream gzip = new GZIPOutputStream(bos);
    OutputStreamWriter osw = new OutputStreamWriter(gzip, StandardCharsets.UTF_8);
    osw.write(s);
    osw.close();
    return bos.toByteArray();
}
 
private static String ungzip(byte[] bytes) throws Exception {
    InputStreamReader isr = new InputStreamReader(new GZIPInputStream(new ByteArrayInputStream(bytes)), StandardCharsets.UTF_8);
    StringWriter sw = new StringWriter();
    char[] chars = new char[1024];
    for (int len; (len = isr.read(chars)) > 0; ) {
        sw.write(chars, 0, len);
    }
    return sw.toString();
}

```

### Go

``` Go

func gzip(w io.Writer, data []byte) error {
    gw, err := gzip.NewWriterLevel(w, gzip.BestSpeed)
    defer gw.Close()
    gw.Write(data)
    return err
}
 
func ungzip(w io.Writer, data []byte) error {
    gr, err := gzip.NewReader(bytes.NewBuffer(data))
    defer gr.Close()
    data, err = ioutil.ReadAll(gr)
    if err != nil {
        return err
    }
    w.Write(data)
    return nil
}

```


### Python

``` python

gzip.compress(data, compresslevel=9)
gzip.decompress(data)

```

