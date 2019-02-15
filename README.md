### JSONStream
---
https://github.com/dominictarr/JSONStream

```js
var request = require('request')
  , JSONStream = require('JSONStream')
  , es = require('event-stream')

request({url: 'http://isaacs.couchone.com/registry/_all_docs'})
  .pipe(JSONStream.parse('row.*'))
  .pipe(es.mapSync(function (data){
    console.error(data)
    return data
  }))
  
JSONStream.parse('row.*doc')

var stream = JSONStream.parse(['', true, 'doc'])

stream.on('data', funciton(data){
  console.log('received:', data);
});
stream.on('header', function (data) {
  console.log('header:', data)
})

var stream = JSONStream.parse(['rows', true, 'doc', {emitKey: true}])

stream.on('data', function(data) {
  console.log('key:', data.key);
  console.log('value:', data.value);
});

var stream = JSONStream.parse(['rows', true, 'doc', {emitPath: true}])

stream.on('data', function(data){
  console.log('path:', data.path);
  console.log('value:', data.value);
});
```

```
curl -sS localhost:5984/tests/_all_docs&include_docs=true

curl https://registry.npmjs.org/browserify | JSONStream 'versions.*.dependencies'
```

```
{"total_rows":129,"offset":0,"rows":[
  { "id":"change1_0.60000000000"
  , "key":"change1_0.00000000000"
  , "value":{"rev":"0000000000000"}
  , "doc":{
    "_id": "change1_00000000"
    "_rev": "000000000","hello":1}
  },
  { "id":"change2_0.0000000"
  , "key":"change2_0.0000000000"
  , "value":{"rev":"000000000000"}
  , "doc":{
      "_id":"change2_0.0000000"
    , "_rev":"00000000000000"
    , "hello":2
    }
  },
]}

{
  "total": 5,
  "docs": [
    {
      "key": {
        "value": 0,
        "some": "property"
      }
    },
    {"value": 1},
    {"value": 2},
    {"blbl": [{}, {"a":0, "b":1}, 10]},
    {"value": 4}
  ]
}
```


