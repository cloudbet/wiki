---
title: Examples
date: 2024-05-22
description: >
  Examples showing how to query the Cloudbet API
type: docs
weight: 2
---

There are several steps to fetching odds from the Cloudbet Feed API and using these to place bets afterwards with the Cloudbet Trading API. Here, we will show you how to fetch these odds after creating a Cloudbet Trading or Affiliate API Key.

In general you would follow these steps to get the latest odds:

1. Get details about upcoming events for your desired sports. The Events or Fixtures endpoint can be used to get a list of upcoming events and competitions for a specific sport on a specific date.

2. Obtain odds for all events of an upcoming competition that you found from the fixtures endpoint by accessing the competitions endpoint. This allows you to batch ingest odds for multiple events if desired. There is also an event endpoint if you want to get odds for a specific event.

## Sports Fixtures

Information about listed events is what we refer to as “fixtures”. We break these down into sports, competitions and events that can be queried from the feed API.

Please substitute `X-API-Key` with your actual Cloudbet API key.

### List of sports

Get a list of sports. Sports are ordered by alphabetical order.

```sh
curl -X "GET" "https://sports-api.cloudbet.com/pub/v2/odds/sports" \
-H "accept: application/json" \
-H "X-API-Key: <API Key>"
-H "Content-Type: application/json"
```

Sample response:

```json
    {
        "sports": [
            {
                "name": "American Football",
                "key": "american-football",
                "competitionCount": 2,
                "eventCount": 92
            },
            {
                "name": "Archery",
                "key": "archery",
                "competitionCount": 0,
                "eventCount": 0
            },
            .
            .
            .
            {
                "name": "Soccer",
                "key": "soccer",
                "competitionCount": 142,
                "eventCount": 1239
            }
        ]
    }
```

### Competitions for a given sport

Get active competitions for a sport. Competitions are grouped by categories.

```sh
curl -X "GET" "https://sports-api.cloudbet.com/pub/v2/odds/sports" \
-H "accept: application/json" \
-H "X-API-Key: <API Key>"
-H "Content-Type: application/json"
```

Sample response:

```json
{
    "name": "Soccer",
    "key": "soccer",
    "competitionCount": 141,
    "eventCount": 1240,
    "categories": [
    {
        "name": "England",
        "key": "england",
        "competitions": [
            {
                "name": "Premier League",
                "key": "soccer-england-premier-league",
                "eventCount": 29
            },
            {
                "name": "FA Cup",
                "key": "soccer-england-fa-cup",
                "eventCount": 3
            },
            .
            .
            .
        ]
    },
    {
        "name": "International",
        "key": "international",
        "competitions": [
            {
                "name": "UEFA Euro 2024",
                "key": "soccer-international-euro-cup",
                "eventCount": 146
            },
            {
                "name": "World Cup",
                "key": "soccer-international-world-cup",
                "eventCount": 1
            },
            .
            .
            .
        ]
    ]
}
```

### Fixtures for a given competition

- Fetch Match Odds, Asian Handicap and Total Goals markets for EPL

```sh
curl -X "GET" "https://sports-api.cloudbet.com/pub/v2/odds/competitions/soccer-england-premier-league?markets=soccer.matchOdds&markets=soccer.asianHandicap&markets=soccer.totalGoals" \
-H "accept: application/json" \
-H "X-API-Key: <API Key>"
-H "Content-Type: application/json"
```

- Fetch Moneyline, Totals and Run Line markets for MLB:

```sh
curl -X "GET" "https://sports-api.cloudbet.com/pub/v2/odds/competitions/baseball-usa-mlb?markets=baseball.moneyline&markets=baseball.totals&markets=baseball.runLine" \
-H "accept: application/json" \
-H "X-API-Key: <API Key>"
-H "Content-Type: application/json"
```

Sample response for NBA with Moneyline and Handicap markets:

```json
{
  "name": "NBA",
  "key": "basketball-usa-nba",
  "sport": {
    "name": "Basketball",
    "key": "basketball"
  },
  "events": [
    {
      "sequence": "97",
      "id": 6473660,
      "home": {
        "name": "Miami Heat",
        "key": "c672-miami-heat",
        "abbreviation": "MIA"
      },
      "away": {
        "name": "Los Angeles Lakers",
        "key": "c655-los-angeles-lakers",
        "abbreviation": "LAL"
      },
      "players": {
        "c4a879-jared-dudley": {
          "name": "Jared Dudley",
          "team": "AWAY",
          "position": {
            "name": "F",
            "key": "f"
          }
        },
        "c4b25d-andre-drummond": {
          "name": "Andre Drummond",
          "team": "AWAY",
          "position": {
            "name": "C",
            "key": "c"
          }
        },
        .
        .
        .
      },
      "status": "TRADING_LIVE",
      "markets": {
        "basketball.handicap": {
          "submarkets": {
            "period=ot&period=ft": {
              "sequence": "97",
              "selections": [
                {
                  "outcome": "home",
                  "params": "handicap=-8",
                  "price": 1.915,
                  "minStake": 0.0001,
                  "probability": 0.505,
                  "status": "SELECTION_ENABLED",
                  "side": "BACK"
                },
                {
                  "outcome": "away",
                  "params": "handicap=-8",
                  "price": 1.95,
                  "minStake": 0.0001,
                  "probability": 0.495,
                  "status": "SELECTION_ENABLED",
                  "side": "BACK"
                },
                {
                  "outcome": "home",
                  "params": "handicap=-10",
                  "price": 2.248,
                  "minStake": 0.0001,
                  "probability": 0.427,
                  "status": "SELECTION_ENABLED",
                  "side": "BACK"
                },
                {
                  "outcome": "away",
                  "params": "handicap=-10",
                  "price": 1.672,
                  "minStake": 0.0001,
                  "probability": 0.573,
                  "status": "SELECTION_ENABLED",
                  "side": "BACK"
                },
                .
                .
                .
              ]
            }
          },
          "liability": 1262.505
        },
        "basketball.moneyline": {
          "submarkets": {
            "period=ot&period=ft": {
              "sequence": "97",
              "selections": [
                {
                  "outcome": "home",
                  "params": "",
                  "price": 1.264,
                  "minStake": 0.0001,
                  "probability": 0.76,
                  "status": "SELECTION_ENABLED",
                  "side": "BACK"
                },
                {
                  "outcome": "away",
                  "params": "",
                  "price": 4.001,
                  "minStake": 0.0001,
                  "probability": 0.24,
                  "status": "SELECTION_ENABLED",
                  "side": "BACK"
                }
              ]
            }
          },
          "liability": 631.2525
        },
      },
      "name": "Miami Heat V Los Angeles Lakers",
      "key": "c672-miami-heat-v-c655-los-angeles-lakers",
      "cutoffTime": "2021-04-08T23:30:00Z",
      "metadata": {
        "opinion": []
      },
      "startTime": "2021-04-08T23:30:00Z"
    },
    {
      "sequence": "1873",
      "id": 5030846,
      "home": null,
      "away": null,
      "players": {
          .
          .
          .
      },
      "status": "TRADING",
      "markets": {
      .
      .
      .
      },
      "name": "NBA - Awards - Coach Of The Year (reg. season)",
      "key": "nba-awards-coach-of-the-year-reg-season",
      "cutoffTime": "2021-04-08T23:30:00Z",
      "metadata": {
        "opinion": []
      },
      "startTime": "2021-04-08T23:30:00Z"
    }
  ]
}
```

### Query a single event

For a single event, the API provides you all available markets. To delve into details about how our markets are structured, please look at the [Cloudbet markets](./markets.md) page.

```sh
curl -X 'GET' "https://sports-api.cloudbet.com/pub/v2/odds/events/6473660" \
-H "accept: application/json" \
-H "X-API-Key: <API Key>" \
-H "Content-Type: application/json"
```

Sample response for a single event

```json
{
  "sequence": "97",
  "id": 6473660,
  "sport": {
    "name": "Basketball",
    "key": "basketball"
  },
  "competition": {
    "name": "NBA",
    "key": "basketball-usa-nba",
    "category": {
      "name": "USA",
      "key": "usa"
    }
  },
  "home": {
    "name": "Miami Heat",
    "key": "c672-miami-heat",
    "abbreviation": "MIA"
  },
  "away": {
    "name": "Los Angeles Lakers",
    "key": "c655-los-angeles-lakers",
    "abbreviation": "LAL"
  },
  "players": {
    "c4a879-jared-dudley": {
      "name": "Jared Dudley",
      "team": "AWAY",
      "position": {
        "name": "F",
        "key": "f"
      }
    },
    "c4b25d-andre-drummond": {
      "name": "Andre Drummond",
      "team": "AWAY",
      "position": {
        "name": "C",
        "key": "c"
      }
    },
    "c4b269-kentavious-caldwell-pope": {
      "name": "Kentavious Caldwell-Pope",
      "team": "AWAY",
      "position": {
        "name": "G",
        "key": "g"
      }
    },
    "c4b58e-ben-mclemore": {
      "name": "Ben McLemore",
      "team": "AWAY",
      "position": {
        "name": "G",
        "key": "g"
      }
    },
    .
    .
    .
  },
  "status": "TRADING",
  "markets": {
    "basketball.handicap": {
      "submarkets": {
        "period=ot&period=ft": {
          "sequence": "97",
          "selections": [
            {
              "outcome": "home",
              "params": "handicap=-8",
              "price": 1.915,
              "minStake": 0.0001,
              "probability": 0.505,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            {
              "outcome": "away",
              "params": "handicap=-8",
              "price": 1.95,
              "minStake": 0.0001,
              "probability": 0.495,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            {
              "outcome": "home",
              "params": "handicap=-10",
              "price": 2.248,
              "minStake": 0.0001,
              "probability": 0.427,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            {
              "outcome": "away",
              "params": "handicap=-10",
              "price": 1.672,
              "minStake": 0.0001,
              "probability": 0.573,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            .
            .
            .
          ]
        }
      },
      "liability": 1262.505
    },
    "basketball.moneyline": {
      "submarkets": {
        "period=ot&period=ft": {
          "sequence": "97",
          "selections": [
            {
              "outcome": "home",
              "params": "",
              "price": 1.264,
              "minStake": 0.0001,
              "probability": 0.76,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            {
              "outcome": "away",
              "params": "",
              "price": 4.001,
              "minStake": 0.0001,
              "probability": 0.24,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            }
          ]
        }
      },
      "liability": 631.2525
    },
    "basketball.totals": {
      "submarkets": {
        "period=ot&period=ft": {
          "sequence": "97",
          "selections": [
            {
              "outcome": "over",
              "params": "total=204.5",
              "price": 1.924,
              "minStake": 0.0001,
              "probability": 0.502,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            {
              "outcome": "under",
              "params": "total=204.5",
              "price": 1.942,
              "minStake": 0.0001,
              "probability": 0.498,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            {
              "outcome": "over",
              "params": "total=202",
              "price": 1.682,
              "minStake": 0.0001,
              "probability": 0.57,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            {
              "outcome": "under",
              "params": "total=202",
              "price": 2.228,
              "minStake": 0.0001,
              "probability": 0.43,
              "status": "SELECTION_ENABLED",
              "side": "BACK"
            },
            .
            .
            .
            .
          ]
        }
      },
      "liability": 420.83500000000004
    }
  },
  "name": "Miami Heat V Los Angeles Lakers",
  "key": "c672-miami-heat-v-c655-los-angeles-lakers",
  "cutoffTime": "2021-04-08T23:30:00Z",
  "metadata": {
    "opinion": []
  },
  "startTime": "2021-04-08T23:30:00Z"
}
```

## Sports Odds

## Account API for Balance Tracking

## Trading API to place bets

## Bet History for settlements
