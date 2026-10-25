# Weather Intelligence — Prototype v0.1

A browser-based UK weather analysis dashboard with actual API connections, four deterministic models, genuine ensemble-member uncertainty, RainViewer historical radar, and an experimental wind-flow visualization.

## Run

Because this is a client-side single-page prototype, start a local web server in the directory:

```bash
python -m http.server 8080
```

Then visit http://localhost:8080 in a modern desktop/mobile browser. Requires an internet connection to third-party APIs and their CDNs. It is also possible to double-click `index.html`, but a local web server is recommended.

## What is live

- UK search and locally saved locations
- Model-derived current-condition values and hourly forecasts
- Independent deterministic guidance from ECMWF, GFS, ICON, and UKMO, served by Open-Meteo
- Actual individual ensemble-member percentiles and threshold exceedance fractions (ECMWF, GEFS, ICON-EPS, UKMO-EPS when the source provides them)
- RainViewer historic rain radar frames
- Experimental wind particle animation from sampled model-predicted wind data
- Data retrieval timestamps, model availability/failure notices, and source links

## Important distinctions

- The so-called current fields from Open-Meteo are **model estimates**, not station measurements.
- Radar returns real remotely sensed precipitation images; these are observations of radar reflectivity, not direct ground rain-gauge quantities.
- Ensemble member exceedance percentages are uncalibrated fractions of the selected model's members, not calibrated objective probabilities.
- Exact forecast model issue timestamps are not exposed by the chosen API calls; retrieval timestamps are shown and explicitly identified as such.
- The wind overlay is a sampled and interpolated particle visualization, not a full high-resolution wind field.
- Some model feeds or ensemble parameters can be unavailable, and the application explicitly shows these failures rather than manufacturing substitute data.

## Data and licences

This prototype accesses Open-Meteo, RainViewer, OpenStreetMap/CARTO map tiles and Chart.js/Leaflet CDN assets. Read provider usage terms before public hosting or commercial deployment; Open-Meteo's non-commercial/free access and RainViewer's public API usage conditions matter. UKMO data can have share-alike obligations. A production release should use a backend ingestion/caching layer and verify all required data redistribution rights.

## Next steps

Add a FastAPI/PostgreSQL service that caches forecasts, records model initialization times where available, stores past model runs and verification against actual rain gauges/stations; add API key/rate control; implement authenticated weather-station contributions and QC flags; wind field on proper gridded data; improved nowcasting; test with real devices on mobile.


## v0.3 changes
- Hour-by-hour deterministic model spread, variable selector and selected-hour control. Close/Moderate/Wide are heuristic agreement bands, **not** forecast probability or validated accuracy.
- Near-location actual rainfall gauges retrieved from the Environment Agency live telemetry API (England only). Gauge readings may be delayed and interval length varies.
- No changes to original radar, maps or weather forecast endpoints.


## v0.4 Atlantic Outlook
Open `atlantic.html` or use the new link from the dashboard. ECMWF/GFS 250hPa wind, 500hPa heights, and MSLP sampled at 40 points across Atlantic; 7-day 6-hour timeline. Map values are point-sampled model forecasts, not full synoptic contours, and are not observations. External Open-Meteo APIs are used directly in browser.
