---
title: API Reference
parent: GetScrape API
nav_order: 1
---

# API Reference

## GET `https://api.rasterwise.com/v1/get-scrape`

This is the main endpoint to use GetScrape. This section contains a description of all the available query parameters to control the API, its behavior and crawl operation and the resulting response.

### Required Parameters

| Parameter | Type   | Description                                                                               | Example                                                                      |
| --------- | ------ | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `apikey`  | string | Your secret API Key. This is required to authenticate your request.                       | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> _-Not an actual apikey-_ |
| `url`     | string | URL of the website / page you want to crawl/scrape. Should start with http:// or https:// | `&url=https://google.com`                                                    |

### Extraction Parameters (Required)

| Parameter | Type   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Example                      |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| `extract` | string | A comma-separated list of entities that you want GetScrape to automatically extract for you. Here is a list of available operations to extract entities: `emails`: extracts email addresses <br> `phones`: extracts US phone numbers <br> `dates`: extracts dates and gives them in ISO format <br> `lists`: extracts html lists (<ol> & <ul>) <br> `headings`: extracts html headings (h1,h2,h3,h4,h5) <br> `images`: extracts url images <br> `links`: extract hyperlinks <br> `rawdom`: gives a raw representation of the DOM | `&extract=dates,lists,links` |
| `scope`   | string | This parameter allows you to pass a selector to scope the crawling operation into a particular DOM node. When passed it will perform the crawling only inside the matched node. Pass DOM element selectors in jQuery fashion. https://api.jquery.com/category/selectors/                                                                                                                                                                                                                                                         | `&scope=#someid > div > li`  |

### Include or Exclude Results with a Matching Word

| Parameter       | Type   |                                                                                                                                                                                                                                                     | Example                  |
| --------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `exclude`       | string | Passing the `exclude` parameter set to a string will exclude results that match that string. For example, `exclude=ads` will exclude any result in the arrays that contain the string `ads`.                                                        | `&exclude=ads`           |
| `exclude_start` | string | Works like `exclude` but it will only exclude strings that start with the passed string. This is useful to exclude data with certain prefixes. For example URL protocols.                                                                           | `&exclude_start=http://` |
| `exclude_end`   | string | Works like `exclude` but it will only exclude strings that end with the passed string. This is useful to exclude data with certain suffixes. For example file formats.                                                                              | `&exclude_end=.svg`      |
| `filter`        | string | Passing the `filter` parameter set to a string will filter results that match that string. For example, `filter=ads` will only include results in the arrays that contain the string `ads`. You can think of `filter` as the opposite of `exclude`. | `&filter=ads`            |
| `filter_start`  | string | Works like `filter` but it will only include strings that start with the passed string. This is useful to only show data with certain prefixes. For example URL protocols.                                                                          | `&filter_start=https://` |
| `filter_end`    | string | Works like `filter` but it will only include strings that end with the passed string. This is useful to only show data with certain suffixes. For example URL protocols.                                                                            | `&filter_start=https://` |

### Drop Results from Start or End of Array

| Parameter    | Type   |                                                                                                                                                                                                  | Example         |
| ------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------- |
| `drop_start` | number | This parameter allows you to drop results in the response by passing a number. For example if you're trying to exclude the first two entities from a result, you can pass `drop_start` set to 2. | `&drop_start=2` |
| `drop_end`   | number | This parameter allows you to drop results in the response by passing a number. For example if you're trying to exclude the last two entities from a result, you can pass `drop_end` set to 2.    | `&drop_end=2`   |

### Get Results with Even or Odd Indexes Only

| Parameter   | Type    |                                                                        | Example           |
| ----------- | ------- | ---------------------------------------------------------------------- | ----------------- |
| `even_only` | boolean | If set to `true` only the results with an even index will be returned. | `&even_only=true` |
| `odd_only`  | boolean | If set to `true` only the results with an odd index will be returned.  | `&odd_only=true`  |

### API Results Workflow

| Parameter | Type   | Description                                                                                                                                                                                             | Example                              |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| `webhook` | string | A valid endpoint URL that can receive and respond to a **POST** request (preferably an endpoint that you control). If set, we will send a **POST** request to the provided endpoint (webhook listener). | `&webhook=https://webhook.myapp.com` |

### Browser Control Parameters

| Parameter  | Type              |                                                                                                                                                                                                                                                                                                                                                                                                   | Example                                                      |
| ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `customjs` | string            | A custom JS evaluation you want to inject before the crawl operation. If passed we will inject this statement as a header `<script>` with a just in time model (script will be injected after loading and before crawling). Useful to force actions that are needed to perform the crawl operation correctly.                                                                                     | `&customjs=document.getElementById("demo"); myobj.remove();` |
| `click`    | array (as string) | The click parameter will dispatch a click at the start of the rendering flow to the passed coordinates or DOM element. For example if you need to click in the coordinates X = 20px and Y = 100px you can pass an array [20, 100. If you need to click on a button or element you can pass the selector of said element. This is helpgul to crawl elements that only render after a click action. | `&click=[20,10]` or `&click=#demobtn`                        |
| `width`    | number            | Width in pixels of the viewport under which the crawl operation is happening. This parameter is helpful to work with pages that change the DOM in narrow viewports which can facilitate the extraction of certain info. Defaults to `1280`                                                                                                                                                        | `&width=1200`                                                |
