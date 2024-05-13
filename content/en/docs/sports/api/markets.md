---
title: Markets
date: 2024-05-13
description: >
  How to work with markets from Cloudbet API Feed and using the corresponding market URLs in the Cloudbet Trading API to place bets.
type: docs
weight: 1
---

- The `market url` can be compiled from the feed and takes the form of `<market_key>/<outcome>?<grouping_parameters>`.

- The `market_key` is the unique identifier for a market and optionally time period with its own settlement rules.

- The `outcome` identifies a unique selection on the market, e.g. `0:0` or `home`.

- `grouping_parameters` include grouping information such as handicap and totals values.

- If no `grouping_parameters` are present (empty string), omit the query string and format as `<market_key>/<outcome>`

- A `line` is determined by the `market_key` and the `grouping_parameters`, all selections on a line sum up to 100% true probability, e.g. `soccer.asian_handicap?handicap=-0.5` includes the home and away outcome.

A list of markets is [available on Github](https://gist.github.com/kgravenreuth/6703e1e213aecac4d5728f2f699d34e7#file-markets-json) and is also made available below.

If you would like to request addition of new markets, then please create a discussion thread in the [Cloudbet Docs Discussions](https://github.com/Cloudbet/docs/discussions) section.

**Full List of available markets on the Cloudbet API**

<script src="https://gist.github.com/kgravenreuth/6703e1e213aecac4d5728f2f699d34e7.js?file=markets.json"></script>
