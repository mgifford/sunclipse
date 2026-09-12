# Sunclipse

**Predicting brilliant sunsights and sunclipses.**

→ [Live site](https://mgifford.github.io/sunclipse/)

A single, self-contained, accessible web page that rates how vivid the next
sunrise or sunset is likely to be (0–100) from your location and live cloud
data.

## Why "sunsight" and "sunclipse"?

The words are [Buckminster Fuller's](https://buckminsterfuller.net/). He
refused to say *sunrise* and *sunset* because they carry a pre-Copernican
picture of the world — as if the Sun rose and fell around a stationary Earth.
It doesn't; the Earth turns. So he coined words built from what actually
happens:

- **Sunsight** — the moment your part of the turning Earth rotates far enough
  for the Sun to come into sight (what we call *sunrise*).
- **Sunclipse** — the moment the Sun is eclipsed by the Earth's horizon as you
  rotate away from it (what we call *sunset*).

He reformed other words the same way — preferring *"in"* and *"out"* to *"up"*
and *"down"*, since gravity pulls toward the Earth's centre. This tool borrows
his vocabulary.

Read more: [Wikipedia](https://en.wikipedia.org/wiki/Buckminster_Fuller) ·
[Buckminster Fuller Institute](https://buckminsterfuller.net/) ·
[Celebrating word-making Buckminster](https://evangriffithnotes.com/celebrating-word-making-buckminster/) ·
[Fuller's 1972 Ford Hall Forum lecture](https://pastdaily.com/buckminster-fuller-has-a-few-words-for-you-1972-ford-hall-forum-lecture-past-daily-weekend-gallimaufry/)

## How the prediction works

At the hour of the next sunsight or sunclipse, the app scores four factors:

| Factor | Weight | What it looks for |
| --- | --- | --- |
| Sunward-horizon low cloud | 40% | A clear horizon toward the Sun (west for a sunclipse, east for a sunsight) so light gets through |
| Overhead cloud canvas | 35% | Partial mid/high cloud (best at 30–70%) to catch and reflect colour |
| Altitude mix | 15% | High cirrus and mid altocumulus reward; heavy local low cloud penalises |
| Atmospheric clarity | 10% | Drier air (<65% RH) and long visibility (>10 km) |

It also shows a viewing timeline (target arrival, local dip/rise, the event
itself, peak cloud burn, and a cutoff) with a live countdown, and an
adjustable slider for how much your local horizon is blocked by trees or hills.

## Accessibility

Built to WCAG 2.2 AA: a high-contrast dark theme (≥4.5:1), visible
`:focus-visible` outlines, 44×44px touch targets, `rem`-based layout that
survives 200% zoom, semantic landmarks and heading hierarchy, `aria-live`
status and prediction regions, and `aria-describedby` links on the data cards.
The coined words are always paired with the familiar ones so no one is left
guessing.

## Deploy

It's one static file. Upload `index.html` to any web host and open it.

- Serve it over **HTTPS** — the precise-GPS button needs a secure origin
  (`https://` or `http://localhost`); it won't work over plain `http://`.
- No server-side code, database, build step, or API key. It works at the site
  root or in any subfolder.

### What the visitor's browser calls at runtime

1. `cdn.jsdelivr.net` — the SunCalc library (solar times)
2. `ipapi.co` — approximate location from the visitor's IP
3. `api.open-meteo.com` — the cloud/weather forecast

All free, all keyless. Your server only serves the HTML file.

To drop the CDN, save `suncalc.js` next to `index.html` and change the
`<script src="…">` tag to `src="suncalc.js"`.
