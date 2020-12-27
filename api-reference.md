---
title: API Reference
nav_order: 1
---

# API Reference

## GET `/v1/get-screenshot`

This is the main endpoint to use GetScreenshot. This section contains a description of all the available query parameters to control the API, its behavior and the resulting captured screenshots.


### Required Parameters

| Parameter | Type   | Description                                                                             | Example                                                           |
|-----------|--------|-----------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| `apikey`    | string | Your secret API Key. This is required to authenticate your request.                     | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> *-Not an actual apikey-* |
| `url`       | string | URL of the website / page you want to screenshot. Should start with http:// or https:// | `&url=https://google.com`                                              |                                    

### Format Parameters

| Parameter | Type   | Description                                                                                                                                                                                                        | Example       |
|-----------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| `format`    | string | The file type/format in which you want to get your capture.  It can be either  `png` or `jpeg`. Defaults to `png`                                                                                                | `&format=png` |
| `pdf`       | string | If set to `true`, any image format will be ignored and instead an A4 PDF of the passed website will be generated. Websites will render the same as if you were printing it from your browser. Defaults to `false` | `&pdf=true`   |

### Dimensions/Viewport Parameters

| Parameter | Type    | Description                                                                                                                                                                                                                 | Example          |
|-----------|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|
| `height`    | number  | Height in pixels of the viewport when taking the page screenshot. Defaults to `800`                                                                                                                                      | `&height=800`    |
| `width`     | number  | Width in pixels of the viewport when taking the page screenshot. Defaults to `1280`                                                                                                                                       | `&width=1200`    |
| `fullpage`  | boolean | If set to `true`, we will calculate the full height of the website and used it as the `height` in pixels of the viewport when taking the page screenshot.   Any passed height value will be ignored. Defaults to `false` | `&fullpage=true` |
| `preset`  | string | If set, we will control the dimension and user-agent to simulate the preset device or graphics display resolution. If a preset value is passed, we will ignore other passed dimension parameters. This parameter can accept any of the following presets: `iphone5` (iPhone 5) <br> `iphone678` (iPhone 6/7/8)<br> `iphone678_plus` (iPhone 6/7/8 +)<br> `iphonex` (iPhone X / XS)<br> `pixel2` (Google Pixel 2)<br> `pixel2_xl` (Google Pixel 2 XL)<br> `ipad` (iPad in Vertical)<br> `ipadpro` (iPad Pro Vertical)<br> `hvga` (320 x 480)<br> `wvga` (480 x 800)<br> `dvga` (640 x 960)<br> `wxga_v` (768 x 1280)<br> `xga` (1024 x 768)<br> `wxga_s` (1280 x 800)<br> `wxga_l` (1366 x 768)<br> `sxga` (1280 x 1024)<br> `wsxga_plus` (1680  x 1050) | `&preset=dvga` | 
| `element` | string | If you need to target specific DOM elements instead of taking dimension-based screenshots you can use the DOM capture parameters to target those elements.  Pass DOM element selectors in jQuery fashion. https://api.jquery.com/category/selectors/ For example. if targeting a div with the id colordiv you can target it by passing the parameter `#colordiv`. | `&element=#colordiv` |

### Modified Rendering Parameters

| Parameter    | Type    | Description                                                                                                                                                                                                                                                                                                   | Example                                                      |
|--------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `highlight`  | string  |  A custom word or phrase you want to highlight. If passed, GetScreenshot will look for that string on the website and highlight all its instances with bright-yellow box.                                                                                                                                     | `&highlight=apple`                                           |
| `customjs`   | string  |  A custom JS evaluation you want to inject before the capture. If passed we will inject this statement as a header <script> with a just in time model, after all the required operations and just before the capture operation. This is important to have in mind when passing JS that changes the rendering. | `&customjs=document.getElementById("demo"); myobj.remove();` |
| `customcss`  | string  |  A custom CSS style you want to inject before the capture. If passed we will inject the style declaration as a header <style> just before the capture operation.                                                                                                                                              | `&customcss=#demo.head12 {color: red !important}`            |
| `hidemsg`    | boolean | If set to true, we will hide message, chat and customer support clients. Currently hides the following clients: Intercom, Drift, Facebook and Tawk (partiallly).  Defaults to false                                                                                                                           | `&hidemsg=true`                                              |
| `hidecookie` | boolean | If set to true, we will hide cookie disclaimers that will usually appear as floating boxes or fixed containers. The hiding is not guaranteed but it has a pretty broad coverage and the underlying hiding heuristic is updated weekly.  Defaults to false                                                     | `&hidecookie=true`                                           |

### Pre-Screenshot Action Parameters

| Parameter | Type              | Description                                                                                                                                                                                                                       | Example          |
|-----------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|
| `click`    | array (as string) | The click parameter will dispatch a click at the start of the rendering flow to the passed coordinates or dom element. For example if you need to click in the coordinates X = 20px and Y = 100px you can pass an array [20, 100. If you need to click on a button or element you can pass the selector of said element. | `&click=[20,10]` or `&click=#demobtn`|

### API Result Workflow Parameters

| Parameter | Type   | Description                                                                                                                                                                                                                                                                                                                                      | Example                              |
|-----------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| `email`     | string | A valid email address. If set, we will send a formatted email to this email address including the captured image and the details of the capture (capture time and URL).                                                                                                                                                                           | `&email=john@example.com`            |
| `webhook`   | string |  A valid endpoint URL that can receive and respond to a **POST** request (preferably an endpoint that you control).  If set, we will send a **POST** request with the final response of the original call, to the provided endpoint (webhook listener).  For your convenience, we send the response in the body and `queryStringParameters` of the request. | `&webhook=https://webhook.myapp.com` |

### Rendering Strategy Parameters

| Parameter | Type   | Description                                                                    | Example       |
|-----------|--------|--------------------------------------------------------------------------------|---------------|
| `strategy`  | number | If set to 1, changes the rendering strategy to our alternative rendering flow. | `&strategy=1` |

<hr>

## GET `/v1/get-screenshot/legacy`

### What is the /legacy API?
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


## GET `/v1/usage`

This endpoint allows you to retrieve your current API usage. This endpoint uses a double security validation and therefore it requires both your registered email and the API Key for which you want to query current usage and available quota.


### Required Parameters

| Parameter | Type   | Description                                                                             | Example                                                           |
|-----------|--------|-----------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| `apikey`    | string | Your secret API Key. This is required to authenticate your request.                     | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> *-Not an actual apikey-* |
| `url`       | string | URL of the website / page you want to screenshot. Should start with http:// or https:// | `&url=https://google.com`                                              |    
