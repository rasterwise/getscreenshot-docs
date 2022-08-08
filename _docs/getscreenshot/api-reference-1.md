---
title: /v1/usage
---

#### Sections in this article
{:.no_toc}
- TOC
{:toc}

### Endpoint

GET `https://api.rasterwise.com/v1/usage`

This endpoint allows you to retrieve your current API usage. This endpoint uses a double security validation and therefore it requires both your registered email and the API Key for which you want to query current usage and available quota.

### Required Parameters

| Parameter | Type   | Description                    | Example                                                                      |
| --------- | ------ | ------------------------------ | ---------------------------------------------------------------------------- |
| `apikey`  | string | Your secret API Key.           | `?apikey=5WjESjB72Rb2JC7frBf026kBgg82DaPQIOxc` <br> _-Not an actual apikey-_ |
| `email`   | string | Email address for the account. | `&email=john@doe.com`                                                        |
