# Natural Events Tracker

An interactive 3D globe of natural events happening on Earth right now: wildfires, severe storms, volcanoes, sea and lake ice, floods and more. It pulls live data from NASA's Earth Observatory Natural Event Tracker (EONET) every time you load or refresh the page.

**Live demo:** _add your GitHub Pages link here once it is published_

Built as a vibe-coded web app with a live API for a data visualization course.

## What it does

- **Live data.** Fetches open events from the NASA EONET v3 API in the browser. No API key is needed.
- **Globe and flat map.** A draggable globe (MapLibre GL JS) that flattens into a normal map as you zoom in. A button on the map switches between globe and flat views.
- **One icon per event type.** Wildfires, storms, volcanoes, ice, floods, earthquakes, drought, dust and haze, landslides, human-made events, snow, temperature extremes and water color each get their own icon in a ring of the type's color.
- **Size aura.** A soft glow behind each icon shows the event's reported size. Fire acreage and ice area are drawn to scale. Storm glow follows wind speed (scaled for effect, not a true storm radius). A faint halo means no size was reported.
- **Readable place names.** Events read like "Wildfire in Perth, Australia" instead of NASA's "Wildfire in Australia 1033662". Storms, volcanoes and icebergs keep NASA's own names, with the nearby town shown underneath.
- **Controls that call the API again.** Status (happening now, ended, all) and time range (7 days to any time) each fetch fresh data. A Refresh button does too.
- **Filters and summary.** Four summary cards, a clickable event-type list that filters the map, and an event list that flies the globe to the event you click.
- **Dark theme** throughout, including the map.
- **Clear errors.** Network failures, timeouts, server errors and malformed responses each show a specific message with a "Try again" button.

## Run it

It is a single HTML file with no build step.

1. Download `index.html`.
2. Open it in a modern desktop browser (Chrome, Edge, Firefox or Safari). An internet connection is required for the NASA data, map tiles, map library and fonts.

Or visit the live demo link above.

## Data source

- **NASA EONET v3:** `https://eonet.gsfc.nasa.gov/api/v3/events`
- Query used: `status` (`open`, `closed` or `all`) and, optionally, `days` (a recent window).
- The sidebar shows how many events NASA returned versus how many were plotted, with a "View raw response" link to the exact URL the app called.

An event is skipped only if it has no usable location. Each event is drawn at its most recent reported position. For events reported as polygons, the app uses the average of the polygon's corner points.

## How place names work

The app does not call a geocoding service. The HTML file contains a list of about 49,000 towns of 5,000+ people (name, latitude, longitude, country, population), and the browser looks up each event's nearest town on load.

- It prefers the biggest town within 30 km, so a district of a large city reads as the city.
- Within 20 km of the town it says "in"; farther away it says "near".
- Events more than 300 km from any listed town (open ocean, remote areas) keep NASA's wording.
- The list is derived from GeoNames. See `THIRD-PARTY.md` for the license and for what was changed.

## Known limitations

- **Place names are approximate.** The nearest town is not the same as the administrative area an event is in, and the town list has gaps in remote regions.
- **Storm glow is not a real storm radius.** EONET gives wind speed, not an area.
- **Many events report no size** (volcanoes and floods, for example), so they show the faint halo.
- **Only the latest position is plotted** for events that move; storm tracks appear as dashed lines.
- **Emoji icons are drawn by your device's emoji font**, so they look slightly different on Windows, Mac and Android.
- **The map needs WebGL.** If it cannot start, the app shows a message and the event list still works.

## Testing

During development the app was exercised in a headless browser with mocked API responses covering: network failure, HTTP 500, non-JSON and wrong-shape responses (each with recovery through "Try again"); malformed and hostile event data (missing coordinates, out-of-range values, HTML in titles, `javascript:` links); 5,000 events at once; rapid repeated refreshes; and slow responses arriving after newer ones. The last test found a real bug, where a slow old response could overwrite newer results, which was fixed by cancelling superseded requests.

These tests use mocked data. They show how the app behaves under bad input; they do not replace comparing the app's numbers with NASA's own response. To do that comparison, load the app, then use "View raw response" and confirm that the event count matches the sidebar.

## Repository contents

| File | Purpose |
|---|---|
| `index.html` | The whole app: markup, styles, code and the embedded town list |
| `README.md` | This file |
| `LICENSE` | MIT license for the original code |
| `THIRD-PARTY.md` | Credits and licenses for data, libraries and services |
| `docs/screenshot.png` | Screenshot used above (add your own) |

## Credits

Event data from [NASA EONET](https://eonet.gsfc.nasa.gov/). Place names from [GeoNames](https://www.geonames.org/). Full details in [`THIRD-PARTY.md`](THIRD-PARTY.md).

## License

Original code is released under the [MIT License](LICENSE). Third-party components keep their own licenses.
