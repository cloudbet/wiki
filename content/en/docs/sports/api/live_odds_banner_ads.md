---
title: Live Odds Banner Ads
description: Embedding live event odds in HTML5 banners using the Cloudbet Sports API
type: docs
weight: 99
---

Live odds banners can display dynamic betting data in HTML5 ad creatives by querying the Cloudbet Sports API. These banners are typically deployed by partners via self-hosted static sites, requiring a proxy layer to comply with CORS restrictions and keep secrets secure if used.

> Note: HTML5 banners cannot directly access Cloudbet APIs from the browser due to CORS. You **must** host a proxy that forwards requests to the Cloudbet Sports API from the same domain.

## API Access

There are two main routes to access the Cloudbet Sports API for this purpose:

1. **Public routes** use `/sports-api/c/v6/....` and do not require an API key.
2. **Private routes** use `/sports-api/v6/....` and require an API key.

Public `/c/` routes are cached, private proxies hit live data but add latency; pick based on freshness needs.

### 1. Use Public Routes without API Key

Example URL:
```plain
https://www.cloudbet.com/sports-api/c/v6/sports/competitions/
    soccer-england-premier-league/events?
    markets=soccer.match_odds
    &markets=soccer.asian_handicap
    &markets=soccer.total_goals
    &locale=en
    &include-pretrading=false
    &limit=1
```

Use a simple static redirect to `/api/...` on your host. You can skip over the private routes example and API key section if you're using this approach (recommended).

#### CORS Proxy Configuration

Browsers enforce same-origin policy on fetch and XHR. Your proxy must include:

```plain
Access-Control-Allow-Origin: *
```

Your hosting must forward e.g. `/api/*` to Cloudbet and inject CORS headers. Example for Netlify (`netlify.toml`) using a static redirect to public endpoints `/c/` where no API key is required:

```toml
[[headers]]
  for = "/api/*"
    [headers.values]
      Access-Control-Allow-Origin = "*"

[[redirects]]
  from = "/api/*"
  to   = "https://www.cloudbet.com/sports-api/c/v6/sports/competitions/:splat"
  status = 200
  force  = true
  headers = {Access-Control-Allow-Origin = "*"}
```

Other options:
- Vercel (`vercel.json` headers & redirects)
- Firebase Hosting (`firebase.json` rewrites + `headers`)
- AWS S3 + CloudFront (`CORSConfiguration`)

Adjust per provider so browser fetches from `/api/...` without errors.

### 2. Use Real-time Routes with API Key

To use real-time odds, partners must create an API key from their Cloudbet player or affiliate account via the self-serve account menu. For this purpose, the API keys are interchangable. Refer to [API Key Access and Examples](/docs/sports/api/examples/) for setup steps and sample requests.

> Ensure that API keys and secrets stay on your server or proxy. **Avoid embedding them in client code**.

Use your proxy to add the `X-API-Key` header when forwarding requests. You can do this with e.g. Netlify functions, AWS Lambda, or Vercel serverless functions. Below is an example of a Netlify function that proxies requests to the Cloudbet Sports API.

```js
import fetch from 'node-fetch';

export async function handler(event) {
  const match = event.rawUrl.match(/\/api(\/.*)/);
  const [ , pathAndQuery ] = match || [];
  const url = `https://www.cloudbet.com/sports-api/v6${pathAndQuery}`;

  const resp = await fetch(url, {
    headers: { 'X-API-Key': process.env.CLOUDBET_API_KEY }
  });

  const body = await resp.json();
  return {
    statusCode: resp.status,
    headers: {
      'Access-Control-Allow-Origin': '*',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(body)
  };
}
```

Set `CLOUDBET_API_KEY` in Netlify’s environment variables. And ensure the cross-origin header is set in the response:

```plain
Access-Control-Allow-Origin: *
```

## HTML5 Banner Integration

Banners should be designed with placeholder text for outcomes and odds, which are dynamically updated at runtime using AJAX calls.

```html
<div id="homeTeam">…</div>
<div id="homeOdds">…</div>
<div id="awayTeam">…</div>
<div id="awayOdds">…</div>
```
Below is a simplified integration flow.

### Building the Request Path

Use the competition endpoint to fetch the next event (`&limit=1`) and desired markets:

```js
const params = new URLSearchParams(location.search);
const locale = params.get('locale') || 'en';
const compKey = 'soccer-england-premier-league';
const markets = ['soccer.match_odds','soccer.asian_handicap','soccer.total_goals'];
const path = `/api/sports/competitions/${compKey}/events?` +
  markets.map(m => `markets=${m}`).join('&') +
  `&locale=${locale}&limit=1`;
```

### Fetch and Render

Include this in your banner’s `<script>`:

```js
document.addEventListener('DOMContentLoaded', () => {
  fetch(path)
    .then(res => res.json())
    .then(data => {
      const e = data.events[0];
      const ah = e.markets['soccer.asian_handicap']
                  .submarkets['period=ft'].selections;
      const homeSel = ah.find(s => s.outcome === 'home');
      const awaySel = ah.find(s => s.outcome === 'away');

      document.getElementById('homeTeam').textContent = e.home.name;
      document.getElementById('awayTeam').textContent = e.away.name;
      document.getElementById('homeOdds').textContent = homeSel.price;
      document.getElementById('awayOdds').textContent = awaySel.price;
    })
    .catch(console.error);
});
```

Swap the market key (`soccer.match_odds` or `soccer.total_goals`) as needed.

### Market Structure Reference

Each market in the response follows:

```json
"markets": {
  "soccer.asian_handicap": {
    "submarkets": {
      "period=ft": {
        "selections": [
          { "outcome": "home", "price": 1.846, "params": "handicap=-0.25" },
          { "outcome": "away", "price": 2.015, "params": "handicap=-0.25" }
        ]
      }
    }
  },
  "soccer.match_odds":   { /* similar */ },
  "soccer.total_goals":  { /* similar */ }
}
```

Extract the `price` field from the `home` and `away` selections.

### Tips and Alternatives

- Use public `/c/v6` routes when no API key is needed.
- For private data or real-time freshness, proxy with key injection.
- Competition endpoint batches events; `limit=1` returns the next match.
- Event endpoint (`/api/events/{id}`) targets a single event.
- Append `&locale=…` for localized team names.

## Summary

Deploying live odds banners requires:

- Self-hosted access with a reverse proxy (CORS handling)
- HTML5 creatives with placeholders for odds
- Minimal JS for fetching and rendering data dynamically

This setup gives affiliates flexible, real-time betting widgets embeddable across any platform or campaign. See these references for more details:

- [API Key & Examples](/docs/sports/api/examples/)
- [Swagger/OpenAPI Documentation](https://cloudbet.com/api)
- [Community Discussions & Questions](https://github.com/cloudbet/docs/discussions/)
