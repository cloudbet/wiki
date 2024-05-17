---
title: Markets
date: 2024-05-13
description: >
  How to work with markets from Cloudbet API Feed and using the corresponding market URLs in the Cloudbet Trading API to place bets.
type: docs
weight: 1
---

### Terminology

#### Market Key

- The `market_key` is the unique identifier for a market and optionally time period with its own settlement rules.

- The `submarket_key` is a logical period grouping of the market selections and is primarily useful as an indicator of when the market is settled. It is not required for the definition of a `line` as explained below.

**Market and Submarket Key Example**

```json
"markets": {
  "soccer.asian_handicap": {
    "submarkets": {
      "period=ft": {
        "sequence": "4441",
        "selections": [
          {
...
```

#### Outcomes, Grouping Parameters and Lines

- The `outcome` identifies a unique selection on the market, e.g. `0:0` or `home`.

- `grouping_parameters` include grouping information such as handicap and totals values.

- If no `grouping_parameters` are present (empty string), omit the query string and format as `<market_key>/<outcome>`

- A `line` is determined by the `market_key` and the `grouping_parameters`, all selections on a line sum up to 100% true probability, e.g. `soccer.asian_handicap?handicap=-0.5` includes the home and away outcome.

**Outcomes, Grouping Parameters and Lines Example**

```json
"selections": [
  {
    "outcome": "home",
    "params": "handicap=-0.75",
    "price": 1.98,
    "minStake": 0.1,
    "maxStake": 13386.98032,
    "probability": 0.488,
    "status": "SELECTION_ENABLED",
    "side": "BACK"
  }
...
```

#### Market URL

The `market url` can be compiled from the feed and takes the form of `<market_key>/<outcome>?<grouping_parameters>`. This can be sent in the payload of the [`/v3/bets/place` endpoint](https://www.cloudbet.com/api/?urls.primaryName=Trading#/Trading/PlaceBet) when placing a bet.

**Market URL Example**

```json
"marketUrl": soccer.total_goals/over?total=3
```

#### Split and Variables

This is static information available in our market list below, while it is not provided dynamically on the Cloudbet API. This information is primarily meant for market settlement, but can also be used by you to visually separate markets by using the Cloudbet Feed API, if you use our API to display markets on your website.

- `Split`: List of periods and teams which affect market settlement.

- `Variables`: List of variables which affect settlement of a specific market. These can also be used to visually separate lines, e.g. the handicap values on an Asian Handicap market.

**Split and Variables Example**

```json
	"soccer.asian_handicap_period_extratime": {
		"Name": "Asian Handicap - Extra Time",
		"Variables": [
			"handicap"
		],
		"Split": "period=et",
		"Outcomes": {
			"away": "{{away}} {{-handicap}}",
			"home": "{{home}} {{handicap}}"
		}
	},
```

A list of markets is [available on Github](https://gist.github.com/kgravenreuth/6703e1e213aecac4d5728f2f699d34e7#file-markets-json) and is also made available below.

If you would like to request addition of new markets, then please create a discussion thread in the [Cloudbet Docs Discussions](https://github.com/Cloudbet/docs/discussions) section.

**Full List of available markets on the Cloudbet API**

<script src="https://gist.github.com/kgravenreuth/6703e1e213aecac4d5728f2f699d34e7.js?file=markets.json"></script>
