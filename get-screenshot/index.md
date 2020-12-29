---
title: Getting Started
parent: GetScreenshot API
nav_order: 1
---

# Getting Started With GetScreenshot

*How to get started with GetScreenshot simple API (5-10 mins) and start generating screenshots via the GET API.*

Generating screenshots just requires a single request to the GetScreenshot API. 
By design, GetScreenshot only supports GET requests. In our experience this favors simplicity, usability and newbie friendliness.
However, if you're interested in POST requests, please let us know since we have a Beta version of our endpoint that supports POST requests.

Here are some examples on how to generate a basic screenshot in the GetScreenshot API with some popular programming languages:

### cURL
```
curl -X GET \
  'https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY' \
  -H 'Auth: allow' \
  -H 'cache-control: no-cache'
```

### JavaScript 



```js
var data = null;

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY");
xhr.setRequestHeader("Auth", "allow");
xhr.setRequestHeader("cache-control", "no-cache");
xhr.setRequestHeader("Postman-Token", "d93809f4-c1b1-4549-8456-36bb75995c75");

xhr.send(data);
```



### NodeJS

```js
var request = require("request");

var options = { method: 'GET',
  url: 'https://api.rasterwise.com/v1/get-screenshot',
  qs: 
   { url: 'https://www.apple.com',
     apikey: 'REPLACE_WITH_YOUR_API_KEY' },
  headers: 
   { 'cache-control': 'no-cache',
     Auth: 'allow' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```



### Ruby


	

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["Auth"] = 'allow'
request["cache-control"] = 'no-cache'

response = http.request(request)
puts response.read_body
```



### Python 



```python
import http.client

conn = http.client.HTTPConnection("api,rasterwise,com")

payload = ""

headers = {
    'Auth': "allow",
    'cache-control': "no-cache",
    }

conn.request("GET", "v1,get-screenshot", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```



### Java



```java
OkHttpClient client = new OkHttpClient();

Request request = new Request.Builder()
  .url("https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY")
  .get()
  .addHeader("Auth", "allow")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
```



### Go



```go
package main

import (
	"fmt"
	"net/http"
	"io/ioutil"
)

func main() {

	url := "https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY"

	req, _ := http.NewRequest("GET", url, nil)

	req.Header.Add("Auth", "allow")
	req.Header.Add("cache-control", "no-cache")

	res, _ := http.DefaultClient.Do(req)

	defer res.Body.Close()
	body, _ := ioutil.ReadAll(res.Body)

	fmt.Println(res)
	fmt.Println(string(body))

}
```



### PHP



```php
<?php

$request = new HttpRequest();
$request->setUrl('https://api.rasterwise.com/v1/get-screenshot');
$request->setMethod(HTTP_METH_GET);

$request->setQueryData(array(
  'url' => 'https://www.apple.com',
  'apikey' => 'REPLACE_WITH_YOUR_API_KEY'
));

$request->setHeaders(array(
  'Postman-Token' => '873e63bb-89f2-49f9-a2e2-99a6b5ec44af',
  'cache-control' => 'no-cache',
  'Auth' => 'allow'
));

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```



### C#



```c#
var client = new RestClient("https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY");
var request = new RestRequest(Method.GET);
request.AddHeader("cache-control", "no-cache");
request.AddHeader("Auth", "allow");
IRestResponse response = client.Execute(request);
```



The code snippets above should be enough to get started and generate a simple 1280 x 800 pixels screenshots of any live website. The base example is a good start to start adding other parameters that control the outcome (generated screenshot).
