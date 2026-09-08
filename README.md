# 🌐 Seismic Trip Radar

Plan around earthquake risk **before you travel.** Enter an itinerary — places and dates — and it maps the seismic activity that overlaps each stop's location and time window, with local emergency numbers attached.

Every other earthquake app answers "is there a quake near me *right now*." This one answers "should I worry about the places I'm *about to go*." It's a trip-planning tool, not a live alerter.

## What it does

For each stop in your itinerary, it:

1. Geocodes the place via Nominatim (OpenStreetMap).
2. Queries USGS for quakes within your radius, during your stay, above a magnitude floor — filtered server-side.
3. Plots everything on a map — stop pins, alert-radius circles, and quake markers sized by magnitude (Leaflet + free CARTO/OSM tiles).
4. Attaches context — country flag and dialing code from REST Countries, plus a bundled emergency-number lookup.

All APIs are free and keyless. No build step, no backend, no dependencies beyond Leaflet from a CDN.

## Run it

Open `index.html` in any browser. To host free: push to GitHub and enable Pages (Settings -> Pages -> deploy from `main`), or drop it on Netlify/Vercel.

## Usage

One stop per line:

```
Place; arrive YYYY-MM-DD; depart YYYY-MM-DD
```

Dates optional — a bare `Place` scans the next 30 days. Tune min magnitude (default 4.5) and radius (default 300 km). Click any stop card to fly the map to it.

## Notes & limits

- Nominatim: 1 request/second and a real User-Agent required. The app throttles and caches per session.
- Emergency numbers are best-effort (REST Countries doesn't provide them). Always verify locally — in an emergency call the number posted where you are.
- "Near" is a judgment call. M4.5 within 300 km is a starting point. It shows recent/historical quakes in your window, not predictions — no one can forecast quakes.
- Client-side only, subject to each API's CORS policy (all three currently allow browser requests).

## Data & attribution

- Earthquakes: USGS Earthquake FDSN (public domain)
- Geocoding & tiles: (c) OpenStreetMap contributors, tiles by CARTO
- Country data: REST Countries
- Map: Leaflet

## License

MIT — do whatever you want, no warranty.
