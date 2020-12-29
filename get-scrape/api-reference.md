---
title: API Reference
parent: GetScrape API
nav_order: 1
---

# API Reference

## GET `/v1/get-scrape`

This is the main endpoint to use GetScrape. This section contains a description of all the available query parameters to control the API, its behavior and crawl operation and the resulting response.


### Required Parameters

| Parameter | Type   | Description                                                                             | Example                                                           |
|-----------|--------|-----------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| `apikey`    | string | Your secret API Key. This is required to authenticate your request.                     | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> *-Not an actual apikey-* |
| `url`       | string | URL of the website / page you want to crawl/scrape. Should start with http:// or https:// | `&url=https://google.com`                                              |                                    

### Extaction Parameter

| Parameter | Type   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Example       |
|-----------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| extract   | string | A comma-separated list of entities that you want GetScrape to automatically extract for you. Here is a list of available operations to extract entities: `emails`: extracts email addresses <br> `phones`: extracts US phone numbers <br> `dates`: extracts dates and gives them in ISO format <br> `lists`: extracts html lists (<ol> & <ul>) <br> `headings`: extracts html headings (h1,h2,h3,h4,h5) <br> `images`: extracts url images <br> `links`: extract hyperlinks <br> `rawdom`: gives a raw representation of the DOM | `&extract=dates,lists,links` |
