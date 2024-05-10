---
title: Handicap Odds
date: 2024-05-10
description: >
  How to work with handicap markets on the Cloudbet API.
categories: [Sports API]
tags: [api, docs]
type: docs
weight: 2
---

Special care should be taken when working with all handicap markets.

In the Cloudbet API, the handicap value refers to the home team value and is inverted on the away side.

Example:

```
market_key: “soccer.asian_handicap”
outcome: "away",
params: "handicap=0.5",
price: 3.3
```

![Handicap Odds](/sports/api/handicap_odds.png)
