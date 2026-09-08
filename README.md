# FleetView

**An interactive, time-scrubbable map of WW2 naval battles.**

Drag the timeline and watch fleets move, aircraft strike, guns fire and ships go down — with every position, sortie and loss placed in time and space. Built for people who read Morison and Tully for fun and wondered why nobody had drawn it.

Currently included:

| Campaign | Dates | Ships | Air ops |
|---|---|---|---|
| Battle of Leyte Gulf | 17–28 Oct 1944 | 57 | 24 |
| Operation Rheinübung — the Bismarck chase | 18–28 May 1941 | 23 | 13 |

## Features

- Minute-resolution timeline with playback from 10 min/s to 1 day/s; auto-slows around key events
- Ships drawn by class (battleship / carrier / cruiser / destroyer / submarine glyphs), coloured by task force, with formation flags (48-star, IJN ensign, White Ensign, Kriegsmarine)
- Automatic sea routing around coastlines (Natural Earth 1:10m, A* on a 2–3 km grid)
- Carrier and land-based air strikes flying out, attacking and returning in formation; torpedo runs; gun tracers; sinking flashes
- Day/night terminator computed from the actual date and time
- Bases, airfields and headquarters with the controlling force's insignia; control changes over time
- Event timeline with losses highlighted, running casualty counter, commander cards, Wikipedia links
- Documented vs reconstructed positions distinguished (solid vs dotted routes, popup confidence note)
- Follow-a-ship, search, keyboard shortcuts, four UI themes (modern / wartime chart × light / dark)

Deep links: `index.html#s=bismarck&t=1941-05-27T10:30`

## Running it

It's a single file. Open `index.html` in a browser, or serve the folder with any static host (GitHub Pages, Cloudflare Pages, Netlify).

Runtime dependencies (loaded from CDNs, none installed):

- [Leaflet](https://leafletjs.com/) 1.9 (BSD-2)
- [world-atlas](https://github.com/topojson/world-atlas) Natural Earth 1:10m land (public domain) via jsDelivr — used for sea routing; the app falls back to straight legs if unavailable
- Esri World Ocean basemap tiles (attribution required)

## Data

All scenario data lives in the `<script>` block at the top of `index.html` (to be split into `data/*.json`). Each scenario is a plain object:

```
ROUTES   named base tracks: [ 'DD HH:MM', lat, lon, note?, 'S'|'R'? ]
SHIPS    { id, name, force, type, route, until?, extra?, sunk?, sunkBy?, lost? }
STRIKES  { from:{route}|{lat,lon}, target:{ship}|{lat,lon}, launch, arrive, leave, recover, count, land?, oneway? }
TORPEDOES, ENGAGEMENTS (gun targets), EVENTS, PORTS (bases / airfields / HQ), COMMANDERS, WIKI
```

Times are in the scenario's zone time (Tokyo UTC+9 for Leyte; ~UTC+2 for the Bismarck chase). Positions of battles and sinkings are taken from published records; transit legs between documented fixes are reconstructions and are drawn dotted.

### Sources

- Samuel Eliot Morison, *History of United States Naval Operations in World War II*, vols. X and XII
- Anthony Tully, *Battle of Surigao Strait*; combinedfleet.com Tabular Records of Movement
- Dictionary of American Naval Fighting Ships (DANFS); Naval History and Heritage Command H-Grams
- Ludovic Kennedy, *Pursuit*; Iain Ballantyne, *Killing the Bismarck*; naval-history.net
- Wikipedia articles for individual ships (linked from each ship's popup)

Corrections and new scenarios are very welcome — open an issue or a pull request.

## Licence

- **Code:** MIT — see `LICENSE`
- **Curated data (routes, events, notes):** [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — see `LICENSE-DATA.md`
- Basemap © Esri and contributors; coastlines Natural Earth (public domain); flags and insignia drawn for this project

This is a non-commercial history project. It carries no advertising and collects no data.
