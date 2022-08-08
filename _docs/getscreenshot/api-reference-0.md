---
title: /v1/get-screenshot
---

#### Sections in this reference
{:.no_toc}
- TOC
{:toc}

### Endpoint

GET `https://api.rasterwise.com/v1/get-screenshot`

Use this endpoint to invoke the API and modify the request with the parameters below.

### Required Parameters

| Parameter | Type   | Description                                                                             | Example                                                                      |
| --------- | ------ | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `apikey`  | string | Your secret API Key. This is required to authenticate your request.                     | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> _-Not an actual apikey-_ |
| `url`     | string | URL of the website / page you want to screenshot. Should start with http:// or https:// | `&url=https://google.com`                                                    |

### Format Parameters

| Parameter       | Type    | Description                                                                                                                                                                                                       | Example               |
| --------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| `format`        | string  | The file type/format in which you want to get your capture. It can be either `png` or `jpeg`. Defaults to `png`                                                                                                   | `&format=png`         |
| `pdf`           | string  | If set to `true`, any image format will be ignored and instead an A4 PDF of the passed website will be generated. Websites will render the same as if you were printing it from your browser. Defaults to `false` | `&pdf=true`           |
| `urlasfilename` | boolean | By default GetScreenshot return screenshots with a random filename. If this parameter is set to `true`, the resulting screenshot filename will contain the target screenshot URL. Defaults to `false`             | `&urlasfilename=true` |

### Dimensions/Viewport Parameters

| Parameter      | Type                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Example              |
| -------------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| `height`       | number                | Height in pixels of the viewport when taking the page screenshot. Defaults to `800`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | `&height=800`        |
| `width`        | number                | Width in pixels of the viewport when taking the page screenshot. Defaults to `1280`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | `&width=1200`        |
| `fullpage`     | boolean               | If set to `true`, we will calculate the full height of the website and used it as the `height` in pixels of the viewport when taking the page screenshot. Any passed height value will be ignored. Defaults to `false`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `&fullpage=true`     |
| `preset`       | string                | If set, we will control the dimension and user-agent to simulate the preset device or graphics display resolution. If a preset value is passed, we will ignore other passed dimension parameters. This parameter can accept any of the following presets: `iphone5` (iPhone 5) <br> `iphone678` (iPhone 6/7/8)<br> `iphone678_plus` (iPhone 6/7/8 +)<br> `iphonex` (iPhone X / XS)<br> `iphone12` (iPhone 12 / 13)<br> `pixel2` (Google Pixel 2)<br> `pixel2_xl` (Google Pixel 2 XL)<br> `ipad` (iPad in Vertical)<br> `ipadpro` (iPad Pro Vertical)<br> `hvga` (320 x 480)<br> `wvga` (480 x 800)<br> `dvga` (640 x 960)<br> `wxga_v` (768 x 1280)<br> `xga` (1024 x 768)<br> `wxga_s` (1280 x 800)<br> `wxga_l` (1366 x 768)<br> `sxga` (1280 x 1024)<br> `wsxga_plus` (1680 x 1050) | `&preset=dvga`       |
| `devicefactor` | number                | Changes the device scale factor. If set to a higher value will result in a higher device pixel ratio. Defaults to `1`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `&devicefactor=2`    |
| `noheight`     | boolean               | Allows `fullpage` parameter to overwrite preset height. This parameter is meant to be used with in combination with a `preset` and `fullpage=true`. Defaults to `false`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `&noheight=true`     |
| `element`      | string (CSS selector) | If you need to target specific DOM elements instead of taking dimension-based screenshots you can use the DOM capture parameters to target those elements. Pass DOM element selectors in [CSS Selector fashion](https://api.jquery.com/category/selectors/). For example. if targeting a div with the id colordiv you can target it by passing the parameter `#colordiv`.                                                                                                                                                                                                                                                                                                                                                                                                              | `&element=#colordiv` |

### Modified Rendering Parameters

| Parameter     | Type                  | Description                                                                                                                                                                                                                                                                                                  | Example                           |
| ------------- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------- |
| `highlight`   | string                | A custom word or phrase you want to highlight. If passed, GetScreenshot will look for that string on the website and highlight all its instances with bright-yellow box.                                                                                                                                     | `&highlight=apple`                |
| `customjs`    | string                | A custom JS evaluation you want to inject before the capture. If passed we will inject this statement as a header <script> with a just in time model, after all the required operations and just before the capture operation. This is important to have in mind when passing JS that changes the rendering. | `&customjs=alert("Injected JS");` |
| `customcss`   | string                | A custom CSS style you want to inject before the capture. If passed we will inject the style declaration as a header <style> just before the capture operation.                                                                                                                                              | `&customcss=#demo {color: red }`  |
| `hidemsg`     | boolean               | If set to `true`, we will hide message, chat and customer support clients. Currently hides the following clients: Intercom, Drift, Facebook and Tawk (partiallly). Defaults to `false`                                                                                                                       | `&hidemsg=true`                   |
| `hidecookie`  | boolean               | If set to `true`, we will hide cookie disclaimers that will usually appear as floating boxes or fixed containers. The hiding is not guaranteed but it has a pretty broad coverage and the underlying hiding heuristic is updated weekly. Defaults to `false`                                                 | `&hidecookie=true`                |
| `hideelement` | string (CSS selector) | Allows you to hide a page element by passing its element selectors in [CSS Selector fashion](https://api.jquery.com/category/selectors/). For example. if you want to hide a div with the id "ad_div" you can do so by passing the parameter `#ad_div`.                                                      | `&hideelement=#ad_div`            |
| `forcetr`     | boolean               | If set to `true`, the website background will be forced to be transparent. Defaults to `false`                                                                                                                                                                                                               | `&forcetr=true`                   |

### Pre-Screenshot Action and Browser Config Parameters

| Parameter | Type              | Description                                                                                                                                                                                                                                                                                                              | Example                                       |
| --------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------- |
| `click`   | array (as string) | The click parameter will dispatch a click at the start of the rendering flow to the passed coordinates or dom element. For example if you need to click in the coordinates X = 20px and Y = 100px you can pass an array [20, 100. If you need to click on a button or element you can pass the selector of said element. | `&click=[20,10]` or `&click=#demobtn`         |
| `cookie`  | string            | Allows you to set a cookie by passing it's key and value in a comma separated fashion.                                                                                                                                                                                                                                   | `&cookie=session,31239e81293undb1db2hgr812gr` |

### API Result Workflow Parameters

| Parameter | Type   | Description                                                                                                                                                                                                                                                                                                                                              | Example                              |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| `email`   | string | A valid email address. If set, we will send a formatted email to this email address including the captured image and the details of the capture (capture time and URL).                                                                                                                                                                                  | `&email=john@example.com`            |
| `webhook` | string | A valid endpoint URL that can receive and respond to a **POST** request (preferably an endpoint that you control). If set, we will send a **POST** request with the final response of the original call, to the provided endpoint (webhook listener). For your convenience, we send the response in the body and `queryStringParameters` of the request. | `&webhook=https://webhook.myapp.com` |

### Rendering Strategy Parameters

| Parameter  | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Example          |
| ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| `strategy` | number | If set to `1` or `2`, changes the rendering strategy to one of our alternative rendering flows. If the default rendering strategy fails to produce an accurate screenshot, we recommend experimenting with this parameter since it will in many cases fix ad-hoc rendering issues that are not covered by the standard rendering technique.                                                                                                                                                                                                                                                                                                                                                                                                                                         | `&strategy=1`    |
| `timewait` | number | This parameter receives an extra time wait in ms. GetScreenshot goes through a rendering execution flow that optimizes for accuracy. To accomplish this, the execution flow introduces arbitrary waits that fix common rendering issues. However, there are instances in which an extra wait will be required to deliver a correct screenshot. In particular websites that perform some extended operation. To address this we make this parameter available so you can increase the wait period before taking the screenshot. We recommend starting at `5000` with `1000` increments. However be advised that our endpoint times out at 30 seconds, so using this parameter will increase the chances of your call timing out. Use this parameter with caution. Defaults to `2000` | `&timewait=5000` |

### Bypass Login Parameters

_Note: Before using the bypass login functionality please have in mind that this is a highly experimental feature and its stability or reliability isn't guaranteed._

Our bypass login strategy depends on instuction data that needs to be passed to the `bplogin` param as a URL encoded string. The instruction data needed is the following:

- Login Page URL
- Username (or email) needed to bypass the login.
- Password needed to bypass the login.
- Username Field CSS Selector
- Password CSS Selector

To pass this data you need to form an encoded comma separated string. For example an instruction like the following `https://example.com/login,jj@example.com,24h3dnfbnkjbnf,input#user,input#password` should ultimately be passed as `https%3A%2F%2Fexample.com%2Flogin%2Cjj%40example.com%2C24h3dnfbnkjbnf%2Cinput%23user%2Cinput%23password`.

Needless to say that this feature should be used carefully since you will be passing credentials for an online resource. Make sure that you understand the risks of revealing authentication data to any third party. Although your credentials are never logged into our systems and they only exist in memory for the duration of the screenshot process, we highly recommend that you only give us credentials that were created for the specific purpose of being handed to and used by GetScreenshot as part of your screenshot needs.

Please **DO NOT** pass credentials that are being used regularly by you or any other person in a day to day authentication context. If you insist on passing your personal credentials, please remember that GetScreenshot is not responsible for their misuse since we don't control the whole end to end life cycle of your requests.

GetScreenshot will use the instruction data to authenticate against the protected website and then will navigate to the target URL to finish the screenshot operation.

If you have questions about this feature please don't hesitate to contact us at support@rasterwise.com

| Parameter | Type               | Description                                                                                                                    | Example                                                                                              |
| --------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| `bplogin` | URL Encoded String | An encoded comma separated string with login url, username, password, username field CSS selector, password field CSS selector | `&bplogin=example.com%2Flogin%2Cjj%40example.com%2C24h3dnfbnkjbnf%2Cinput%23user%2Cinput%23password` |

### Bypass Login Instruction

NOTE: This guide is mostly tailored for Zapier Users

If you are a Zapier user you may not be entirely sure on how to form a bypass instruction. Don't worry forming an instruction that can be used in the context of Zapier is quite simple.

If you need to bypass a login through Zapier you need to provide the following information in a comma separated format:

- Login Page URL
- Username (or email) needed to bypass the login.
- Password needed to bypass the login.
- Username Field CSS Selector
- Password CSS Selector

This will result in an instruction that looks similar to the following: `https://example.com/login,jj@example.com,24h3dnfbnkjbnf,input#user,input#password`.

Although the first three values (login url, username and password) are quite straight-forward you might not know what's a CSS selector and how to get it.
Fortunately CSS selectors are quite simple. CSS Selectors are identifiers that point to an element in a website UI. In this case you need to tell GetScreenshot
the fields in which to enter the username and password you provided in the first two fields.

To obtain the CSS selectors you just need to do a small operation in your browser. Here is a quick YouTube video that explains how to do it: [How to Get CSS Selector](https://www.youtube.com/watch?v=GMk7ZLuo6Po)

When copying the CSS selector of the username field and password field, make sure you're actually copying the selector of the actual form field. Most likely this would be a `<input>` element in both cases.

If you have any questions please reach out to support@rasterwise.com
s