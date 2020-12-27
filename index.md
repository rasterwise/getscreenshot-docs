# GetScreenshot Documentation and API Reference

- [Getting Started With GetScreenshot](https://github.com/rasterwise/getscreenshot-docs/blob/main/README.md#getting-started-with-getscreenshot)
- [Authentication](https://github.com/rasterwise/getscreenshot-docs#authentication)
- [API Reference](https://github.com/rasterwise/getscreenshot-docs/blob/main/README.md#api-reference)

## Getting Started With GetScreenshot

*How to get started with GetScreenshot simple API (5-10 mins) and start generating screenshots via the GET API.*

Generating screenshots just requires a single request to the GetScreenshot API. 
By design, GetScreenshot only supports GET requests. In our experience this favors simplicity, usability and newbie friendliness.
However, if you're interested in POST requests, please let us know since we have a Beta version of our endpoint that supports POST requests.

Here are some examples on how to generate a basic screenshot in the GetScreenshot API with some popular programming languages:

### cURL
<details>
<summary>
Code Example
</summary>
<p>

```
curl -X GET \
  'https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY' \
  -H 'Auth: allow' \
  -H 'cache-control: no-cache'
```

</p>
</details>

### JavaScript 

<details>
<summary>
Code Example
</summary>
<p>

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

</p>
</details>

### NodeJS

<details>
<summary>
Code Example
</summary>
<p>


```
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

</p>
</details>

### Ruby

<details>
<summary>
Code Example
</summary>
<p>
	

```
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

</p>
</details>

### Python 

<details>
<summary>
Code Example
</summary>
<p>

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

</p>
</details>

### Java

<details>
<summary>
Code Example
</summary>
<p>

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

</p>
</details>

### Go

<details>
<summary>
Code Example
</summary>
<p>

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

</p>
</details>

### PHP

<details>
<summary>
Code Example
</summary>
<p>

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

</p>
</details>

### C#

<details>
<summary>
Code Example
</summary>
<p>

```c#
var client = new RestClient("https://api.rasterwise.com/v1/get-screenshot?url=https://www.apple.com&apikey=REPLACE_WITH_YOUR_API_KEY");
var request = new RestRequest(Method.GET);
request.AddHeader("cache-control", "no-cache");
request.AddHeader("Auth", "allow");
IRestResponse response = client.Execute(request);
```

</p>
</details>

The code snippets above should be enough to get started and generate a simple 1280 x 800 pixels screenshots of any live website. The base example is a good start to start adding other parameters that control the outcome (generated screenshot).

## Authentication

To authenticate requests when using the API you need to pass your secret API key by using they `apikey` query parameter in your request. You do not need to provide a password.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail. 

You will receive your secret API key via email when you register for any of the available plans. 
If you don't receive your API key or you lose it you can always automatically ask for a new one from [here](https://getscreenshot.rasterwise.com/account.html). GetScreenshot will send you a new email with the API Key.

Your API keys carry many privileges, so be sure to keep them secret! Do not share your secret API keys in publicly accessible places like GitHub, client-side implementations, forums, etc.

If for some reason you believe your API Key was compromised, please contact us immediately at support@rasterwise.com.

## API Reference

### GET `/v1/get-screenshot`

This is the main endpoint to use GetScreenshot. This section contains a description of all the available query parameters to control the API, its behavior and the resulting captured screenshots.


#### Required Parameters

| Parameter | Type   | Description                                                                             | Example                                                           |
|-----------|--------|-----------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| `apikey`    | string | Your secret API Key. This is required to authenticate your request.                     | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> *-Not an actual apikey-* |
| `url`       | string | URL of the website / page you want to screenshot. Should start with http:// or https:// | `&url=https://google.com`                                              |                                    

#### Format Parameters

| Parameter | Type   | Description                                                                                                                                                                                                        | Example       |
|-----------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| `format`    | string | The file type/format in which you want to get your capture.  It can be either  `png` or `jpeg`. Defaults to `png`                                                                                                | `&format=png` |
| `pdf`       | string | If set to `true`, any image format will be ignored and instead an A4 PDF of the passed website will be generated. Websites will render the same as if you were printing it from your browser. Defaults to `false` | `&pdf=true`   |

#### Dimensions/Viewport Parameters

| Parameter | Type    | Description                                                                                                                                                                                                                 | Example          |
|-----------|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|
| `height`    | number  | Height in pixels of the viewport when taking the page screenshot. Defaults to `800`                                                                                                                                      | `&height=800`    |
| `width`     | number  | Width in pixels of the viewport when taking the page screenshot. Defaults to `1280`                                                                                                                                       | `&width=1200`    |
| `fullpage`  | boolean | If set to `true`, we will calculate the full height of the website and used it as the `height` in pixels of the viewport when taking the page screenshot.   Any passed height value will be ignored. Defaults to `false` | `&fullpage=true` |
| `preset`  | string | If set, we will control the dimension and user-agent to simulate the preset device or graphics display resolution. If a preset value is passed, we will ignore other passed dimension parameters. This parameter can accept any of the following presets: `iphone5` (iPhone 5) <br> `iphone678` (iPhone 6/7/8)<br> `iphone678_plus` (iPhone 6/7/8 +)<br> `iphonex` (iPhone X / XS)<br> `pixel2` (Google Pixel 2)<br> `pixel2_xl` (Google Pixel 2 XL)<br> `ipad` (iPad in Vertical)<br> `ipadpro` (iPad Pro Vertical)<br> `hvga` (320 x 480)<br> `wvga` (480 x 800)<br> `dvga` (640 x 960)<br> `wxga_v` (768 x 1280)<br> `xga` (1024 x 768)<br> `wxga_s` (1280 x 800)<br> `wxga_l` (1366 x 768)<br> `sxga` (1280 x 1024)<br> `wsxga_plus` (1680  x 1050) | `&preset=dvga` | 
| `element` | string | If you need to target specific DOM elements instead of taking dimension-based screenshots you can use the DOM capture parameters to target those elements.  Pass DOM element selectors in jQuery fashion. https://api.jquery.com/category/selectors/ For example. if targeting a div with the id colordiv you can target it by passing the parameter `#colordiv`. | `&element=#colordiv` |

#### Modified Rendering Parameters

| Parameter    | Type    | Description                                                                                                                                                                                                                                                                                                   | Example                                                      |
|--------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `highlight`  | string  |  A custom word or phrase you want to highlight. If passed, GetScreenshot will look for that string on the website and highlight all its instances with bright-yellow box.                                                                                                                                     | `&highlight=apple`                                           |
| `customjs`   | string  |  A custom JS evaluation you want to inject before the capture. If passed we will inject this statement as a header <script> with a just in time model, after all the required operations and just before the capture operation. This is important to have in mind when passing JS that changes the rendering. | `&customjs=document.getElementById("demo"); myobj.remove();` |
| `customcss`  | string  |  A custom CSS style you want to inject before the capture. If passed we will inject the style declaration as a header <style> just before the capture operation.                                                                                                                                              | `&customcss=#demo.head12 {color: red !important}`            |
| `hidemsg`    | boolean | If set to true, we will hide message, chat and customer support clients. Currently hides the following clients: Intercom, Drift, Facebook and Tawk (partiallly).  Defaults to false                                                                                                                           | `&hidemsg=true`                                              |
| `hidecookie` | boolean | If set to true, we will hide cookie disclaimers that will usually appear as floating boxes or fixed containers. The hiding is not guaranteed but it has a pretty broad coverage and the underlying hiding heuristic is updated weekly.  Defaults to false                                                     | `&hidecookie=true`                                           |

#### Pre-Screenshot Action Parameters

| Parameter | Type              | Description                                                                                                                                                                                                                       | Example          |
|-----------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|
| `click`    | array (as string) | The click parameter will dispatch a click at the start of the rendering flow to the passed coordinates or dom element. For example if you need to click in the coordinates X = 20px and Y = 100px you can pass an array [20, 100. If you need to click on a button or element you can pass the selector of said element. | `&click=[20,10]` or `&click=#demobtn`|

#### API Result Workflow Parameters

| Parameter | Type   | Description                                                                                                                                                                                                                                                                                                                                      | Example                              |
|-----------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| `email`     | string | A valid email address. If set, we will send a formatted email to this email address including the captured image and the details of the capture (capture time and URL).                                                                                                                                                                           | `&email=john@example.com`            |
| `webhook`   | string |  A valid endpoint URL that can receive and respond to a **POST** request (preferably an endpoint that you control).  If set, we will send a **POST** request with the final response of the original call, to the provided endpoint (webhook listener).  For your convenience, we send the response in the body and `queryStringParameters` of the request. | `&webhook=https://webhook.myapp.com` |

#### Rendering Strategy Parameters

| Parameter | Type   | Description                                                                    | Example       |
|-----------|--------|--------------------------------------------------------------------------------|---------------|
| `strategy`  | number | If set to 1, changes the rendering strategy to our alternative rendering flow. | `&strategy=1` |

<hr>

### GET `/v1/get-screenshot/legacy`

#### What is the /legacy API?
GetScreenshot is built on top of the latest versions of Puppeteer+Chromium. With the pass of time Puppeteer and Chromium have improved their performance resulting in a more reliable and consistent API.

However, due to changes in Puppeteer's recent versions, some of our old rendering strategies are not possible anymore.

We have been working hard in trying to keep the same rendering coverage as the previous version. Still, we ended up in a situation where we improved many pending rendering scenarios, but we also regressed in a couple.

We think this is unlikely to affect anyone since we are talking about just a couple of obscure rendering scenarios that seem to be specific to very particular website implementations. However, if it happens to be that the new API breaks your case (again, this is highly unlikely), we still want to give you the option to access the previous version. We are also hopeful that the folks at Google will fix some of the issues that caused the case regressions, so we don't have to rely on the legacy API anymore.

#### For how long would the /legacy API be available?
Again, we can't stress enough that it is unlikely that you will need to use this API at all. This API is built on top of NodeJS 8.X, and its availability it's contingent on our cloud provider supporting this runtime in the long run. We expect the API to be available for at least another full year (maybe more).

#### What methods are not available in the /legacy API?
The following methods are **NOT** available in the /legacy API:

- `click`
- `strategy`

<hr>


### GET `/v1/usage`

This endpoint allows you to retrieve your current API usage. This endpoint uses a double security validation and therefore it requires both your registered email and the API Key for which you want to query current usage and available quota.


#### Required Parameters

| Parameter | Type   | Description                                                                             | Example                                                           |
|-----------|--------|-----------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| `apikey`    | string | Your secret API Key. This is required to authenticate your request.                     | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> *-Not an actual apikey-* |
| `url`       | string | URL of the website / page you want to screenshot. Should start with http:// or https:// | `&url=https://google.com`                                              |    

<hr>

## API Overview

A brief explanation of the technical details of the GetScreenshot API.

### GET Model

GetScreenshot is a RESTful API that can be accessed by any standard/popular client with HTTP capabilities. This means that almost any language with an HTTP request library o built-in module can make calls to GetScreenshot.

A successful request to the GetScreenshot API will return a simple JSON that includes a URL pointing to the resulting screen capture.

By design, GetScreenshot only uses a GET / URL query parameter model. We intentionally designed the API this way to favor usability, low-effort implementations and beginner developer friendliness. There's also a tiny performance improvement when using GET requests instead of POST, but we didn't consider this when designing  the API.

Although we believe a GET endpoint is the right approach for this type of service, we understand that there are situations (for security / or architecture reasons) where passing formed JSON payloads to a POST API is necessary. We don't have that functionality yet, but we want to support it if there's enough customer appetite for it. If you are interested in this please contact us to support@rasterwise.com

### Speed

GetScreenshot is heavily optimized to return a response in as little time as possible. However is important to understand that the underlying operation is equivalent to navigating to any website from a Chrome Browser tab. 

GetScreenshot will make several optimizations under the hood, but it will only be as fast as the website you're trying to load.

In general terms, the size of a website shouldn't have a noticeable impact on the API response times, since GetScreenshot operates on top of a server with a throughput of 10 Gbps. 

However, GetScreenshot needs to make scrolling operations and controlled wait times in order to reveal all the DOM elements. This will have an impact on the speed of the response depending on the size of the DOM that you're trying to capture.

In practice GetScreenshot API response times take in average 8000-12000 ms for simple websites and 15000 to 22000 ms for complex websites.

Have in mind that after 30000 ms the API will timeout regardless of what's happening in the server. It's extremely rare for GetScreenshot to go over 30 seconds. If your website is very complex and indeed takes more than 30 seconds to get captured, our standard solution might not be a good fit for your case. 
We can provide a dedicated endpoint for your business with a custom timeout. If you're interested on this, please contact us.

### API Calls Caching

GetScreenshot API is **NOT** cached. That means that every time you make a call and get a successful response you will get a new fresh capture. We opted to not cache our API to decrease the pricing associated with setting up a cache cluster and cache index. This is reflected in a cheaper API call than other services.

We also opted to not cache our API because we believe ephemeral responses are more secure since we are dealing with a smaller data surface. 
In simple terms what this means is that your request lives only for the time is needed to provide a response. This allows us to offer a service that is easily adaptable to a HIPAA and GDPR compliant architecture.

If you have a need for cached API calls, we can provide a dedicated cached endpoint for an extra monthly fee. This fee covers the price of a 512MB cache cluster and a cache index. If you're interested in something like this please let us know at support@rasterwise.com


### Screenshot Caching and Hotlinking

Screenshots are saved for 30 days in a secure Amazon S3 Bucket. You can access and retrieve your screenshot image as many times as you want with no extra charge during the next 30 days after the screenshot was generated. You can also hotlink to the image but please note that the image will get deleted after 30 days, no exceptions. 

If you need a permanent link to your image we recommend you to use the S3 Bucket Save option. This feature allows you to pass a user/key pair to our API that will be used to save the image to your own Amazon S3 Bucket. This feature is not publicly available, so please contact us for further instructions.

<hr>


## How GetScreenshot Works?

A brief exaplanation and overview of how GetScreenshot renders website pages and capture screenshots.

### How does GetScreenshot capture screenshots?
As many services in this space, GetScreenshot uses Google's Headless Chrome implementation (Puppeteer) to generate your screenshots. 
When you send a request to our service the following things will happen:

- The server will launch a headless Chrome session.
- Then  it will perform a controlled navigation that emulates a common user navigation, based on the preferences set in your request.
- Upon loading the passed website, our script will snap a screenshot and perform any requested post-processing.
- The script will save the screenshot to a secure static storage location (a secure Amazon S3 Bucket).
- The script will send a response back to your client, with the URL of your screenshot.
- You can retrieve the resulting screenshot for the following 30 days. After 30 days, the object will get deleted forever.
- The script that capture screenshots is highly tuned to return accurate renderings. Under the hood GetScreenshot has three capturing modes that cover multiple edge cases. 
- GetScreenshot determines automatically which one is the best fit for the page you're trying to capture and deals with animations, viewport height units, lazy-loaded elements and more.

### Why should I use GetScreenshot instead of writing my own implementation?
We definitely asked this question ourselves when releasing this API. Also there are several other services in this space that offer similar APIs, so it's fair to assume that there's demand for this kind of managed service, so there must be a reason to avoid a self-managed implementation.

We really don't have a concrete answer, but here is what we believe are the top reasons to choose a service like GetScreenshot:

#### - Using Puppeteer is easy. Making it work the right way is hard.

If you decide to go and write your own service on top of Puppeteer you will quickly find how hard is to get its synchronous behavior right. 

It's very likely that you will spend countless hours trying to tweak the execution of your Puppeteer script just to address edge cases. We have already done that, and we keep doing it. We addressed several edge cases and we keep updating our underlying logic to address more.

#### - If your job is to write beautiful and performant code for complex problems, you will hate writing your own implementation of this. 

Sounds over dramatical, but is true. There's nothing glamorous or exciting about writing a screenshot capture service for your own application. You are going to spend countless hours trying to understand why a certain particular DOM element is not showing or why Puppeteer for some reason is capturing a complete white page.

We build GetScreenshot and offer it at a low price point, so you can go and work on the important stuff. 

If you're passionate about this area of work, then we definitely encourage you to go and test writing your own implementation. Otherwise, we encourage you to give us a try.

#### - You actually need to provide infrastructure resources, just for this.

Amazon EC2? Amazon ECS? Digital Ocean Droplet? Google GCE? Heroku App? A Linux Machine in the janitorial closet? 

Whatever it is, you need something to run your own screenshot capture service, and that means dealing with provisioning and paying for under-used resources.

Our recommendation is to not waste time on this and simply go with something already implemented and exposed through a secure RESTful API. That's where we come. At our price point, it's just easier and potentially cheaper. There's no point in managing this yourself.

#### - Your time as a developer is actually more expensive than you think.

Let's say that you are a mid-level developer in a small market earning $90K USD per year, working 40 hours per week. Your effective hour rate is: $47 USD per hour. 
Now, writing your own super basic implementation of this will take at least 5 hours. But that's just getting a simple prototype ready. 

Realistically you can spend +30 hours just trying to address rendering issues, spinning and calibrating resources, creating and exposing a RESTful API, writing documentation, testing, etc. And then you also need to integrate this into whatever you're planning to use, support it, and likely expand it to address some alternative uses. 

So in a realistic scenario, you can easily spend more than a week writing something like this, and then a an hour every month supporting it. That's almost $2000 USD of your time, just to write a service like this, plus another $500 USD or so, just to support it every year. And this doesn't include whatever you're paying to run it.

GetScreenshot P90 of screenshot needs, is about 5000 captures which you can get with a $10 USD a month plan. That's $120 USD a year.

So the question is: What sounds better? Spending +$2500 worth of your time and stress to write a similar service or pay $120 USD to someone else and let them deal with it?
If you're still not convinced about the price, please let us know. We can always work out something based on your specific needs.
