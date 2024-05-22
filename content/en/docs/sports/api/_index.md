---
title: Cloudbet API
linkTitle: API
description: Programmatic access to Cloudbet's sportsbook and services.
weight: 200
type: docs
---

Swagger/OpenAPI documentation can be found at https://www.cloudbet.com/api/

The docs are split into the following sections:

- **Account**: Account management functions
- **Feed**: Real-time sportsbook data
- **Trading**: Trading API
- **Trading B2B**: Trading B2B API enabling you to set your own odds based on the data we supply

## Cloudbet API Keys

### Trading API Key

The Trading API (aka Betting API) is meant for developers who want to place bets and allows you to perform sports betting programatically.

You should deposit the equivalent of 10 EUR in a currency of your choice and can navigate to the [API key section in your account menu](https://www.cloudbet.com/en/player/api). You can generate and revoke keys here in case you leak it, but be careful as there is a penalty for rotating keys too often.

![Cloudbet Trading API Key](/wiki/images/api_key.png)

### Affiliate API Key

The Affiliate API is primarily meant if you want to consume Cloudbet odds without needing to place bets programatically. You can obtain the Cloudbet Affiliate API Key by logging into your Cloudbet Affiliate account and then visiting the Affiliate API Token page. Please note that there are 2 tokens on this page. Make sure to generate the token in the API Key section.

Using this Cloudbet Affiliate API Key you can then go back to https://www.cloudbet.com/api/ to test the Feed API endpoints.

If you authenticate with the Cloudbet Affiliate API Key, then the Feed API responses may be cached and up to 1 minute behind the latest updates. This is in contrast to using the Cloudbet Trading API Key, which gives you real-time updates.
