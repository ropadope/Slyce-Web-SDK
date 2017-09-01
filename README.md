# Getting started

# Non-ui version

## Loading

### Standart method
```html
<script type="text/javascript" src="../dist/slyce.ui.sdk.js"></script>
<link rel="stylesheet" href="../dist/slyce.ui.css">
```
```javascript
 var sdk = new window.slyceSDK();
```

### AMD, CommonJS2, etc...
```javascript
 var slyceSDK = require('../dist/slyce.sdk');
 var sdk = new slyceSDK();
```

### Change enviroment
For use other foundation\pounce server you need to pass env name to contructor
```
    var sdk = new slyceSDK('staging');
```
Envs:
 1. production - default value, all production servers
 2. staging - staging foundation server, production pounce server
 3. dev - staging foundation server, dev pounce server


## methods
### init(clientId)
call to pounce server uid endpoint and init providers, create websocket connection as need

#### Params
 1. clientId - unified id

#### Result
Method return native promise object

 - on resolve - object with result information like this `{ recognition : false, similar: false }`
 - on reject - Error object with text message

#### Example

```javascript
var id = 'superidididid';
sdk.init(id).then(function(data) {
    console.log(data);  // { recognition : true, similar: true }
}, function(error) {
    console.log(error); // Error('Incorrect client id')
});
```

### recognitionByUrl(url, callbackProgress, isUI = true)
call to stocks and foundation websocket

#### Params
1. url - image url
2. callbackProgress - function which called when status changed

#### Result
Method return native promise object
 - on resolve - return array with products list from fastest provider
 - on reject - Error object with text message

#### Example
```javascript
var url = 'http://imageurl.com/image.jpg';
sdk.recognitionByUrl(url,  function(data) {
    console.log(data); // progress event, {"code":8000,"message":"Processing started","progress":20,"token":"d1fL0USvp_ZotmfhmH4Vcw"}
}).then(function(data) {
    console.log(data); // success, product list, [{"itemId":"0024984171","productDescription":"Popover fit, Drawstring hood, Long sleeves, Front kangaroo pocket","productImageURL":"https://pics.ae.com/is/image/aeo/0195_9585_604_f?$pdp-main_small$","productImages":["https://pics.ae.com/is/image/aeo/0195_9585_604_f?$pdp-main_small$"],"productName":"AEO Men's Baja Hooded Sweater (Deep Burgundy)","productPrice":"69.95","productURL":""}]
}, function(data) {
    console.log(data); // Error('Image not found')
});
```

### recognitionByFile(file, callbackProgress, isUI = true)
Rotate, resize and upload image to amazon s3 and then run **recognitionByUrl** method

#### Params
1. file - File, received by <input type="file">
2. canvas - canvas DOM element. If you do not need rotate and resize use **null**
3. callbackProgress - function which called when status changed
#### Result
Same with **recognitionByUrl**

#### Example
```javascript
$('input[type="file"]').on('change', function(e) {
    sdk.recognitionByFile(e.target.files[0], document.getElementById('canvas'),  function(data) { }).then(function(data) {}, function(data) {});
})
```

### similar(keyword, isUI = true)
Call to bluesky provider

#### Params
1. keyword - file url or product pid

#### Result
Native promise object
 - on resolve - return array with products list from bluesky provider
 - on reject - Error object with text message

#### Example
```javascript
sdk.similar(url).then(function(data) {
   console.log(data); // [{},{}]
}, function(data) {
   console.log(data); // Error('Products not found')
});
```


### getSimilar(pid, url, isUI = true)
Call to bluesky provider

#### Params
1. pid - product pid
1. url - file url

#### Result
Native promise object
 - on resolve - return array with products list from bluesky provider
 - on reject - Error object with text message

#### Example
```javascript
sdk.getSimilar(pid, url).then(function(data) {
   console.log(data); // [{},{}]
}, function(data) {
   console.log(data); // Error('Products not found')
});
```



### progressClose()
Close ui view


### track(eventName, params)
Call to statistic service

#### Params
1. eventName - name of event
2. params - object of properties

#### Result
Native promise object
 - on resolve - return array with products list from bluesky provider
 - on reject - Error object with text message

#### Example
```javascript
sdk.track('modalOpen',{ product: 4832 }).then(function(data) {
   console.log('success');
}, function(data) {
   console.log('error');
});
```
