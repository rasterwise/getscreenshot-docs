---
title: Getting Started
parent: GetScrape API
nav_order: 0
---

# Getting Started With GetScrape

*How to get started with GetScape simple API (5-10 mins) and start crawling/scraping via the GET API.*

Performing crawaling/scraping operations just requires a single request to the GetScrape API. 
By design, GetScrape only supports GET requests. In our experience this favors simplicity, usability and newbie friendliness.
However, if you're interested in POST requests, please let us know at support@rasterwise.com

Here are some examples across different languages, of how to generate a scrape operation that extracts all the links of a page in the GetScrape API:

### cURL
```
curl --location --request GET 'https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links'
```

### JavaScript 



```js
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function() {
  if(this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links");

xhr.send();
```



### NodeJS

```js
var request = require('request');
var options = {
  'method': 'GET',
  'url': 'https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links',
  'headers': {
  }
};
request(options, function (error, response) {
  if (error) throw new Error(error);
  console.log(response.body);
});
```



### Ruby


	

```ruby
require "uri"
require "net/http"

url = URI("https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links")

https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true

request = Net::HTTP::Get.new(url)

response = https.request(request)
puts response.read_body
```



### Python 



```python
import http.client

conn = http.client.HTTPSConnection("api.rasterwise.com")
payload = ''
headers = {}
conn.request("GET", "/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```



### Java



```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
Request request = new Request.Builder()
  .url("https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links")
  .method("GET", null)
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

  url := "https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```



### PHP



```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```



### C#



```c#
var client = new RestClient("https://api.rasterwise.com/v1/get-scrape?apikey=REPLACE_WITH_YOUR_API_KEY&url=https://www.apple.com&extract=links");
client.Timeout = -1;
var request = new RestRequest(Method.GET);
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```



The code snippets above should be enough to get started and generate a simple scrape operation that extracts all the links of a page. The base example is a good start to start adding other parameters that control the outcome (crawl/scrape result).
