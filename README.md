# Seismic — Live Earthquake Visualizer

A real-time dashboard of every earthquake recorded by the USGS, plotted on a zoomable world map and refreshed every 5 minutes.

**[View the live dashboard →](https://kartik6049.github.io/earthquake_visualizer/)**

## What it shows

| View | What you see |
| --- | --- |
| **Live stats** | Total events, strongest quake, mean magnitude and deepest quake for the selected window |
| **World map** | One circle per earthquake. Size shows magnitude, colour shows depth, and quakes from the last 3 hours pulse |
| **Details panel** | Click any quake for its time, depth, coordinates, felt reports, tsunami alert and a link to the full USGS report |
| **Magnitude distribution** | How many quakes fall into each magnitude band, showing how small quakes vastly outnumber large ones |
| **Activity over time** | Quakes per hour or per day, revealing bursts such as aftershock sequences |
| **Depth breakdown** | Shallow (< 70 km), intermediate (70–300 km) and deep (> 300 km) events |
| **Strongest events** | A sortable table of the top 10 quakes by magnitude |

**Controls:** choose a time range (past 24 hours, 7 days, 30 days at M2.5+, or significant events), filter by minimum magnitude, scroll to zoom, drag to pan.

## Built with

| Tool | Used for |
| --- | --- |
| [D3.js](https://d3js.org/) | Map projection, scales, data grouping and fast hover lookup (quadtree) |
| HTML Canvas | Drawing thousands of quakes and the pulse animation at 60 fps |
| [TopoJSON](https://github.com/topojson/topojson-client) | Lightweight world map shapes |
| [CanvasJS](https://canvasjs.com/) | Magnitude histogram and activity timeline |
| [Google Charts](https://developers.google.com/chart) | Depth donut chart and top-10 table |

No frameworks and no build step: the whole project is a single `index.html`.

## Data

Live GeoJSON feeds from the [USGS Earthquake Hazards Program](https://earthquake.usgs.gov/earthquakes/feed/). The feeds are free, need no API key, and update every minute; the dashboard re-fetches every 5 minutes.

## How it works

1. World shapes are loaded once and converted to land and border outlines.
2. The selected USGS feed is fetched, cleaned and sorted so smaller quakes draw on top of larger ones.
3. Each quake's coordinates are projected to screen positions once and cached.
4. A `requestAnimationFrame` loop redraws the map every frame, applying zoom and the pulse animation.
5. Hovering uses a D3 quadtree to find the nearest quake instantly, even with thousands of points.

Circle **area** (not radius) tracks magnitude, using a square-root scale so large quakes don't swamp the map.

## Run it locally

```bash
git clone https://github.com/yourusername/earthquake-visualizer.git
cd earthquake-visualizer
# open index.html in your browser, or serve it:
npx serve .
```

An internet connection is needed for the libraries and live data.

## Design

A restrained editorial theme: warm charcoal background, cream text, and a single burnt-orange accent. Depth uses one orange ramp from light (shallow) to dark (deep). Headings use Plus Jakarta Sans; all numbers and labels use JetBrains Mono.

## Ideas for improvement

- Tectonic plate boundaries as a map layer
- USGS PAGER alert levels in the details panel
- A 30-day replay animation
- Browser notifications for M6+ earthquakes
- An accessible data-table fallback for screen readers

## Credits

- Earthquake data: U.S. Geological Survey
- Map data: [world-atlas](https://github.com/topojson/world-atlas) (Natural Earth)
- CanvasJS is free for non-commercial use

Made by **Kartik Sahani** · [LinkedIn](https://www.linkedin.com/in/kartiksahani604900)
