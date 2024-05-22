---
title: Scraping
date: 2024-05-10
description: >
  This section provides guidance on Cloudbet’s approach to scraping.
type: docs
---

Cloudbet supports scraping activities under specific conditions and does not deploy Cloudflare captcha pages by default, regardless of the IP origin, including datacenter IPs. Captcha challenges are only activated when dynamic rate limits are exceeded. These limits are regularly reviewed and adjusted to minimize disruptions and maintain a seamless user experience.

You are encouraged to use the [Cloudbet Feed API](https://www.cloudbet.com/api/) to scrape Cloudbet sports odds. Our Feed API gives you detailed documentation as well as support from Cloudbet representatives and the Cloudbet Community on the [Cloudbet API Discussions Forum](https://github.com/cloudbet/docs/discussions). Such support is not available if you attempt to scrape the Cloudbet website directly.

At the same time, if you want to use a scraping tool such as Puppeteer or Playwright to scrape odds from the Cloudbet website, this is also possible on our platform under specific conditions as mentioned above. However, using such tools is usually much slower and more error prone as compared to using the official Cloudbet API.
