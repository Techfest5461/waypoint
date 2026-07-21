<p align="center">
  <img src="assets/logo-mark.svg" width="88" alt="Waypoint logo">
</p>

<h1 align="center">Waypoint</h1>
<p align="center"><b>Find your next Indian getaway.</b></p>
<p align="center">A single-file, no-build trip recommender that scores 95 hand-researched Indian destinations against your budget, dates, and starting city — then backs every match with live weather, air quality, and travel advisories.</p>

---

## What it does

You tell Waypoint your budget, headcount, travel dates, trip type, and starting city. It scores every destination in its dataset against **twelve weighted factors** — not just "does it fit the budget" — and hands back a ranked, explained shortlist. Pick one and it builds a day-by-day roadmap, a cost breakdown, and pulls **live conditions** for that destination so you know what you're actually walking into.

## Features

**Matching & planning**
- 12-factor weighted scoring engine (100 points): budget utilization, weather suitability, travel distance/cost/time, transport convenience, crowd level, popularity, attractions, nearby destinations, trip-type fit, and trip-length fit
- A "Why this score?" breakdown on every card, showing exactly what each factor contributed and why
- Auto-generated day-by-day itinerary and category-level budget breakdown for whichever destination you pick

**Real-time destination data**
- Live temperature and conditions, and live air-quality index, per destination (Open-Meteo)
- A **Live Conditions** panel that turns those readings — plus today's real date — into plain-language advisories (extreme heat, storms, poor air quality, visiting outside the ideal season), so you see potential problems before you commit to a trip
- Live Wikipedia imagery keyed to the exact article for each place, with graceful fallbacks if an image or API call fails

**Interface**
- Glassmorphism panels, animated gradient/particle backgrounds, and floating ambient blobs
- Boarding-pass-styled trip planner with animated (count-up) stats
- Skeleton loading states and a compass-themed Lottie loader while a search runs
- Confetti on a successful search, card hover/tilt/shine interactions, and an animated search bar
- Fully respects `prefers-reduced-motion` — every decorative animation degrades to static/instant

## Tech stack

Plain HTML, CSS, and vanilla JavaScript in a single file — **no build step, no framework, no bundler.** External dependencies are loaded from CDN at runtime:

| Purpose | Service | Auth needed |
|---|---|---|
| Weather | [Open-Meteo Forecast API](https://open-meteo.com/) | No |
| Air quality | [Open-Meteo Air Quality API](https://open-meteo.com/) | No |
| Destination imagery | [Wikipedia REST API](https://www.mediawiki.org/wiki/API:Main_page) | No |
| Loading animation | [lottie-web](https://github.com/airbnb/lottie-web) (via cdnjs) | No |
| Fonts | Google Fonts (Fraunces, Inter, JetBrains Mono) | No |

## Getting started

There's nothing to install or build.

```bash
git clone https://github.com/<your-org>/waypoint.git
cd waypoint
```

Then either:
- Open `index.html` directly in a browser, or
- Serve it locally so the live-data fetches behave exactly as they would in production:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

All live-data calls (weather, AQI, imagery) require the browser to have internet access — the app degrades gracefully (badges just say "unavailable") if any of them fail or are blocked.

## Project structure

```
waypoint/
├── index.html          # the entire application: markup, styles, and logic
├── assets/
│   ├── logo.svg         # full logo lockup (icon + wordmark), used in this README
│   └── logo-mark.svg    # icon-only mark, used as the favicon source
└── README.md
```

## How the scoring works

Each destination is scored out of 100 across twelve weighted factors:

| Factor | Weight |
|---|---|
| Budget utilization | 15 |
| Weather suitability | 12 |
| Travel distance | 10 |
| Travel cost | 9 |
| Travel time | 8 |
| Crowd level | 8 |
| Popularity | 8 |
| Attractions | 7 |
| Nearby destinations | 6 |
| Trip-type fit | 6 |
| Trip-length fit | 6 |
| Transport option | 5 |

Every sub-score degrades smoothly instead of falling off a cliff (e.g. a destination just outside your ideal season still gets partial credit), so close-but-imperfect matches still rank sensibly. The full breakdown, with a plain-language reason for every point earned, is available on each result card.

## Data & attribution

- Destination facts (cost bands, ideal seasons, ideal trip length, group fit, popularity, attraction count) are hand-researched and indicative, not live-sourced — treat cost figures as planning-level estimates, not quotes.
- Weather and air-quality readings are live and update on every page load; they reflect current conditions, not forecasts for your travel dates.
- Destination photography is fetched live from Wikipedia and © their respective Wikipedia contributors.

## Known limitations

- This is a demo/portfolio project — it has no backend, no persistence, and doesn't store anything you enter.
- The distance/cost/time estimates use straight-line (haversine) distance and simple heuristics, not real routing — treat them as a starting point, not a booking-grade estimate.
- Live-data APIs are free, keyless, and rate-limited by their providers; heavy traffic may see occasional "unavailable" badges.

## Contributing

Issues and pull requests are welcome — in particular, corrections to destination data (costs, seasons, attraction counts) are easy to review and merge since everything lives in a single `PLACES` array in `index.html`.

## License

Add the license of your choice here (e.g. MIT) before publishing.
