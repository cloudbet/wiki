---
title: Cloudbet Sports MCP Server
linkTitle: MCP Integration
description: Query Cloudbet sports data via AI using the Model Context Protocol.
weight: 15
type: docs
---

The Cloudbet Sports MCP Server exposes structured sports betting data to AI models using [Model Context Protocol](https://modelcontextprotocol.io/), enabling natural-language queries mapped to live market data.

## Why MCP?

- Query sports data using plain English
- Receive structured, real-time odds
- Compatible with Claude, OpenAI, and custom AI runtimes
- Open-source, extensible, easy to self-host

## How It Works

The demo server currently implements a single tool via MCP JSON-RPC:

### Tool: `findEventsAndMarketsByCompetition`

Returns upcoming events and primary markets for a fuzzy-matched competition.

**Tool Metadata (`tools/list`):**
```json
{
  "name": "findEventsAndMarketsByCompetition",
  "description": "Finds upcoming events and odds using fuzzy search",
  "inputSchema": {
    "type": "object",
    "properties": {
      "competitionName": { "type": "string" },
      "limit": { "type": "integer" }
    },
    "required": ["competitionName"]
  }
}
```

**Sample Call (`tools/call`):**

```json
{
  "params": {
    "name": "findEventsAndMarketsByCompetition",
    "arguments": {
      "competitionName": "Premier League",
      "limit": 1
    }
  }
}
```

**Sample Response (truncated):**

```json
{
  "structuredContent": [
    {
      "Name": "Liverpool vs. AFC Bournemouth",
      "CutoffTime": "2025-08-15T19:00:00Z",
      "markets": {
        "soccer.match_odds": {
          "submarkets": {
            "period=ft": {
              "selections": [
                {
                  "Outcome": "home",
                  "Price": 1.346,
                  "MaxStake": 574.15,
                  "MarketURL": "soccer.match_odds/home"
                },
                {
                  "Outcome": "draw",
                  "Price": 5.238,
                  "MaxStake": 208.02,
                  "MarketURL": "soccer.match_odds/draw"
                },
                {
                  "Outcome": "away",
                  "Price": 6.711,
                  "MaxStake": 208.02,
                  "MarketURL": "soccer.match_odds/away"
                }
              ]
            }
          }
        },
        "soccer.total_goals": { /* includes over/under, Price, MaxStake */ },
        "soccer.asian_handicap": { /* includes line, sides, Price, MaxStake */ }
      }
    }
  ]
}
```

## Supported Sports & Markets

Primary markets selected per sport:

| Sport      | Markets                                       |
| ---------- | --------------------------------------------- |
| Soccer     | `match_odds`, `asian_handicap`, `total_goals` |
| Basketball | `handicap`, `moneyline`, `totals`             |
| Tennis     | `winner`, `game_handicap`, `total_games`      |
| Others     | NFL, Cricket, MMA, Boxing, Ice Hockey         |

## Natural Language Mapping

Fuzzy search maps user queries to competitions using Levenshtein distance:

| Example Query         | Match                           |
| --------------------- | ------------------------------- |
| “Premier League odds” | `soccer-england-premier-league` |
| “NBA games”           | `basketball-usa-nba`            |
| “Champions League”    | `soccer-uefa-champions-league`  |

## Getting Started

### Self-host

```bash
git clone https://github.com/cloudbet/sports-mcp-server
cd sports-mcp-server
go run .
```

### Claude Integration

```json
{
  "mcpServers": {
    "cloudbet-sports": {
      "command": "go",
      "args": ["run", "main.go"],
      "cwd": "/path/to/sports-mcp-server"
    }
  }
}
```

### CURL Example

```bash
curl -X POST http://localhost:8080/ -H "Content-Type: application/json" -d '{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "findEventsAndMarketsByCompetition",
    "arguments": { "competitionName": "Premier League", "limit": 3 }
  }
}'
```

## Resources

* [MCP Server on GitHub](https://github.com/cloudbet/sports-mcp-server)
* [MCP Protocol Spec](https://modelcontextprotocol.io/)
* [Sports API Examples](/docs/sports/api/examples/)
