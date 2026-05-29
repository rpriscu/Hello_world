# LY5120 Landing Tracker ✈️

A polished, dark-theme single-page web app that shows when **El Al flight LY5120
(Kraków KRK → Tel Aviv TLV)** is going to land — with a live **early / on-time / late**
status badge, a landing countdown, and an animated route map.

Built to be shared as a link so someone can see when the flight lands.

## What it does

- Pulls **best-effort live data** client-side from Flightradar24 JSON via public CORS
  proxies (tried in order, with timeouts and fallback).
- Filters specifically to the **KRK → TLV** leg (the LY5120 number is also used on
  other routes/days), then picks the live / nearest-upcoming / most-recent occurrence.
- Shows **estimated/actual landing time** in Tel Aviv local time, a live countdown,
  and a colour-coded status:
  - 🔵 **Early** &nbsp; 🟢 **On time** &nbsp; 🟠 **Late** &nbsp; 🔴 **Cancelled / Diverted**
- If the live feed can't be reached, it gracefully falls back to the **published
  schedule** (dep 10:55 KRK · arr 14:56 TLV) and links out to live trackers.
- Auto-refreshes every 60s, re-checks on tab focus, fully responsive (phone-first).

## Files

- `site/index.html` — the entire app (self-contained: HTML + CSS + JS, no build step).

## Publishing to here.now

> ⚠️ This repo's Claude Code **web environment blocks the `here.now` host** in its
> network policy, so the site couldn't be auto-published from the cloud session.
> Publish it from your own machine (one command), or loosen the environment's
> network policy to allow `here.now`. See
> https://code.claude.com/docs/en/claude-code-on-the-web

From your local machine with Node installed:

```bash
# 1. install the here.now skill (one-time)
npx skills add heredotnow/skill --skill here-now -g

# 2. publish this folder
~/.agents/skills/here-now/scripts/publish.sh site
```

The script prints a live URL like `https://<slug>.here.now/`. Without an API key the
site is anonymous and expires in 24h; sign in (the script walks you through a one-time
email code) to make it **permanent**, then share the link.

To update later: `~/.agents/skills/here-now/scripts/publish.sh site --slug <slug>`
