---
title: API Overview
parent: GetScreenshot API
nav_order: 2
---

# API Overview

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

Screenshots are saved for 30 days in a secure Amazon S3 Bucket or Google Cloud Storage Bucket. You can access and retrieve your screenshot image as many times as you want with no extra charge during the next 30 days after the screenshot was generated. You can also hotlink to the image but please note that the image will get deleted after 30 days, no exceptions. 

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
