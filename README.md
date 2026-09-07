# 🌍 Disaster-Aware Travel Radar

A single-file web app that checks live **USGS earthquake data** against your travel itinerary — and only alerts you to quakes that actually overlap a stop's **location and dates**, with local emergency numbers attached.

Not another pulsing global quake map. This one knows where *you* are going.

## What it does

For each stop in your itinerary, it:

1. **Geocodes** the place name to coordinates via [Nominatim](https://nominatim.org/) (OpenStreetMap).
2. **Queries [USGS](https://earthquake.usgs.gov/fdsnws/event/1/)** for earthquakes within a radius, during your stay, above a magnitude floor — the filtering happens server-side.
3. **Attaches context** from [REST Countries](https://restcountries.com/) (flag, dialing code) plus a bundled emergency-number dataset.
4. Shows only the quakes that matter, or a clean "no qualifying quakes" note.

All three APIs are **free and keyless**. No build step, no backend, no dependencies.

## Run it

Open `index.html` in any browser. That's it.

To host it free: push to GitHub and enable **GitHub Pages** (Settings → Pages → deploy from `main`), or drop the file on Netlify/Vercel.

## Usage

Enter one stop per line:

```
Place; arrive YYYY-MM-DD; depart YYYY-MM-DD
```

Dates are optional — a bare `Place` scans the next 30 days. Tune the **minimum magnitude** (default 4.5) and **alert radius** (default 300 km) to taste.

## Notes & limits

- **Nominatim allows 1 request/second** and requires a real `User-Agent`. The app throttles geocoding and caches results per session. For heavier use, self-host Nominatim or swap in another geocoder.
- **Emergency numbers are a best-effort bundled dataset** (REST Countries doesn't provide them). Always verify locally — in a real emergency, call the number posted where you are.
- **"Near" is a judgment call.** M4.5 within 300 km is a starting point, not gospel. A distant moderate quake may be irrelevant; a nearby shallow one may not be in the feed instantly.
- Client-side only, so it's subject to each API's CORS policy (all three currently allow browser requests).

## Data & attribution

- Earthquakes: [USGS Earthquake FDSN](https://earthquake.usgs.gov/fdsnws/event/1/) (public domain)
- Geocoding: © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors via Nominatim
- Country data: [REST Countries](https://restcountries.com/)

## License

MIT — do whatever you want, no warranty.
