# Third-party notices

This app uses data, code and services from the sources below. The MIT license in `LICENSE` covers only the original code in this repository, not these components.

## Data

### NASA EONET (Earth Observatory Natural Event Tracker)
- **What:** live natural-event data (type, location, date, size, sources), requested from the browser at runtime.
- **Source:** https://eonet.gsfc.nasa.gov/ (API: `https://eonet.gsfc.nasa.gov/api/v3/events`)
- **Terms:** NASA provides EONET openly and without an API key. See NASA's data and media usage guidelines at https://www.nasa.gov/nasa-brand-center/images-and-media/ for reuse of NASA material. This app is not endorsed by NASA.
- **Not stored:** event data is fetched live and is not included in this repository.

### GeoNames (place names), via the `all-the-cities` package
- **What:** a list of towns used to turn event coordinates into names like "Perth, Australia". It is embedded in `index.html` in a `<script type="text/plain" id="city-data">` block.
- **Source:** GeoNames, https://www.geonames.org/
- **License:** Creative Commons Attribution 4.0 International (CC BY 4.0), https://creativecommons.org/licenses/by/4.0/
- **Obtained through:** the `all-the-cities` npm package, version 3.1.0, which is licensed under MIT. https://www.npmjs.com/package/all-the-cities
- **Changes made (as CC BY 4.0 requires us to state):** the data was filtered to places with a population of 5,000 or more; reduced to name, latitude, longitude, country code and population; coordinates were rounded to two decimal places; population was rounded to thousands; names containing unsafe characters had them replaced with spaces; and the list was sorted by latitude. About 49,000 entries remain.
- **Attribution shown in the app:** the sidebar footer credits GeoNames.

## Code and libraries

### MapLibre GL JS 5.23.0
- **What:** draws the globe, map, icons and glows.
- **License:** BSD 3-Clause
- **Source:** https://maplibre.org/ and https://github.com/maplibre/maplibre-gl-js
- **Delivery:** loaded from the unpkg CDN at runtime. It is not copied into this repository.

### Google Fonts: Bricolage Grotesque and Instrument Sans
- **What:** headline and body typefaces.
- **License:** SIL Open Font License 1.1, https://openfontlicense.org/
- **Source:** https://fonts.google.com/
- **Delivery:** loaded from Google Fonts at runtime. If the fonts cannot load, the page falls back to system fonts.

## Map imagery

### Esri basemap tiles (World Dark Gray Base and Reference)
- **What:** the dark map background and its labels.
- **Source:** Esri, https://www.esri.com/ (tiles served from `server.arcgisonline.com`)
- **Attribution shown in the app:** "Tiles © Esri — Esri, HERE, Garmin, FAO, NOAA, USGS, OpenStreetMap contributors"
- **Note:** the tiles are used without an API key and are subject to Esri's terms of use. Review those terms before using the app in a commercial or high-traffic setting.

## Icons

Event icons are standard Unicode emoji, drawn by the viewer's own device font. No icon files or emoji fonts are included in this repository.

## Development and testing only (not shipped)

- **Playwright** (Apache-2.0) was used to run the app in a headless browser against mocked responses.
