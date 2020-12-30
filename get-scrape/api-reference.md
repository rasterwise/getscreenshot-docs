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

### Extraction Parameter

| Parameter | Type   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Example       |
|-----------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| `extract`   | string | A comma-separated list of entities that you want GetScrape to automatically extract for you. Here is a list of available operations to extract entities: `emails`: extracts email addresses <br> `phones`: extracts US phone numbers <br> `dates`: extracts dates and gives them in ISO format <br> `lists`: extracts html lists (<ol> & <ul>) <br> `headings`: extracts html headings (h1,h2,h3,h4,h5) <br> `images`: extracts url images <br> `links`: extract hyperlinks <br> `rawdom`: gives a raw representation of the DOM | `&extract=dates,lists,links` |


### String Match Reduction Parameters

| Parameter | Type   |                                                                                                                                                                                       | Example        |
|-----------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| `exclude` | string | Passing the `exclude` parameter set to a string will exclude results that match that string. For example, `exclude=ads` will exclude any result in the arrays that contain the string `ads`. | `&exclude=ads` |
| `exclude_start` | string | Works like `exclude` but it will only exclude strings that start with the passed string. This is useful to exclude data with certain prefixes. For example URL protocols. | `&exclude_start=http://` |
| `exclude_end`  | string | Works like `exclude` but it will only exclude strings that end with the passed string. This is useful to exclude data with certain suffixes. For example file formats. | `&exclude_end=.svg`|
| `filter`  | string | Passing the `filter` parameter set to a string will filter results that match that string. For example, `filter=ads` will only include results in the arrays that contain the string `ads`. You can think of `filter` as the opposite of `exclude`. | `&filter=ads`|
| `filter_start` | string | Works like `filter` but it will only include strings that start with the passed string. This is useful to only show data with certain prefixes. For example URL protocols. | `&filter_start=https://` |
| `filter_end` | string | Works like `filter` but it will only include strings that end with the passed string. This is useful to only show data with certain suffixes. For example URL protocols. | `&filter_start=https://` |


### Array Size/Form Reduction Parameters

| Parameter    | Type   |                                                                                                                                                                                                     | Example         |
|--------------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| `drop_start` | number | This parameter allows you to drop results in the response by passing a number. For example if you're trying to exclude the first two entities from a result, you can pass `drop_start` set to 2.  | `&drop_start=2" |
| `drop_end`   | number | This parameter allows you to drop results in the response by passing a number. For example if you're trying to exclude the last two entities from a result, you can pass `drop_end` set to 2.  | `&drop_end=2" |
