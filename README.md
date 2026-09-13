# Sunclipse

**Predicting brilliant sunsights and sunclipses.**

→ [Live site](https://mgifford.github.io/sunclipse/)

A single, self-contained, accessible web page that rates how vivid the next
sunrise or sunset is likely to be (0–100) from your location and live cloud
data — and helps you plan when and where to look.

## Why "sunsight" and "sunclipse"?

The words are [Buckminster Fuller's](https://buckminsterfuller.net/). He refused
to say *sunrise* and *sunset* because they carry a pre-Copernican picture of the
world — as if the Sun rose and fell around a stationary Earth. It doesn't; the
Earth turns. So he coined words built from what actually happens:

- **Sunsight** — the moment your part of the turning Earth rotates far enough for
  the Sun to come into sight (what we call *sunrise*).
- **Sunclipse** — the moment the Sun is eclipsed by the Earth's horizon as you
  rotate away from it (what we call *sunset*).

Read more: [Wikipedia](https://en.wikipedia.org/wiki/Buckminster_Fuller) ·
[Buckminster Fuller Institute](https://buckminsterfuller.net/) ·
[Celebrating word-making Buckminster](https://evangriffithnotes.com/celebrating-word-making-buckminster/) ·
[Fuller's 1972 Ford Hall Forum lecture](https://pastdaily.com/buckminster-fuller-has-a-few-words-for-you-1972-ford-hall-forum-lecture-past-daily-weekend-gallimaufry/)

## Features

- **Sunsight / sunclipse toggle** that defaults to whichever event is *next*
  (pre-dawn → sunsight, daytime → that evening's sunclipse, after dusk →
  tomorrow's sunsight).
- **Three ways to set location:** approximate by IP, precise GPS (with a
  network-accuracy fallback), or a place search (Open-Meteo geocoding). Save
  named places to your browser.
- **True sun direction:** shows the compass bearing where the Sun meets the
  horizon (it's only due E/W at the equinoxes) and samples cloud toward it.
- **Viewing timeline** with a live countdown, and a terrain slider for how much
  your local horizon is blocked by trees or hills.
- **"Since your last visit"** — how the Sun has shifted (time of day + left/
  right) since you last checked that spot, day over day.
- **"Also in the sky"** — moon phase, moonrise/moonset, the twilight windows
  worth going out early or staying late for, and how far your horizon is.
- **Optional satellite cloud map** (Leaflet + a live infrared overlay) — loads
  only when you open it, so the page stays light otherwise.
- **Location-aware times** — every time is shown in the *location's* timezone,
  not your device's.

## How the prediction works

At the hour of the next event, five factors are scored and weighted:

| Factor | Weight | What it looks for |
| --- | --- | --- |
| Sunward-horizon low cloud | 35% | A clear horizon toward the Sun — sampled along a 50/100/150 km corridor, far end weighted most |
| Overhead cloud canvas | 30% | Partial mid/high cloud (best 30–70%) to catch and reflect colour |
| Altitude mix | 10% | High cirrus + mid altocumulus reward; heavy local low cloud penalises |
| Atmospheric clarity | 10% | Drier air (<65% RH) and long visibility (>10 km) |
| Aerosol / smoke | 15% | Thin–moderate aerosol deepens the colour; heavy smoke dulls it |

Any factor with no data drops out and the remaining weights are renormalized.

Bands: 90–100 *Vivid Burn Expected* · 70–89 *High Quality* · 45–69 *Moderate* ·
0–44 *Low / Obscured (Skip)*.

## Data sources (all free, no API key)

- **Solar & lunar times/positions:** [SunCalc](https://github.com/mourner/suncalc)
  (client-side).
- **Cloud, humidity, visibility, elevation, timezone:**
  [Open-Meteo](https://open-meteo.com/) forecast + geocoding APIs.
- **Aerosol optical depth:** Open-Meteo Air Quality API.
- **Satellite cloud overlay (optional map):**
  [RainViewer](https://www.rainviewer.com/) over a
  [CARTO](https://carto.com/) / [OpenStreetMap](https://www.openstreetmap.org/)
  base.

## Accessibility

Built to WCAG 2.2 AA: high-contrast dark theme (≥4.5:1), visible
`:focus-visible` outlines, 44×44 px touch targets, `rem`-based layout that
survives 200 % zoom, semantic landmarks and heading order, `aria-live` status
and prediction regions, and `aria-describedby` on the data cards. Coined words
are always paired with the familiar ones, and the satellite map is an *optional
visual extra* — the text cloud figures remain the accessible source of truth.

## Sustainability

No framework, no build step, no tracking, system fonts. The satellite map's
library and tiles load only on request. (A response-caching pass to cut repeat
API calls is a planned improvement.)

## Deploy

It's one static file. Upload `index.html` to any web host and open it.

- Serve it over **HTTPS** — the precise-GPS button needs a secure origin.
- No server-side code, database, build step, or API key. Works at the site root
  or any subfolder.

To drop the SunCalc CDN dependency, save `suncalc.js` next to `index.html` and
change the `<script src="…">` tag to `src="suncalc.js"`.

## Licence

[GNU Affero General Public License v3.0](LICENSE) (AGPL-3.0). Fork freely,
modify, and distribute — provided your modifications, including any offered over
a network, remain open source under the same licence.
