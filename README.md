# FleetView

**An interactive, time-scrubbable map of WW2 naval battles.**

**▶ Live site: https://bread40k.github.io/fleetview/**

Drag the timeline and watch fleets move, aircraft strike, guns fire and ships go down — with every position, sortie and loss placed in time and space. Built for people who read Morison and Tully for fun and wondered why nobody had drawn it.

Currently included:

| Campaign | Dates | Ships | Air ops |
|---|---|---|---|
| Battle of Leyte Gulf | 17–28 Oct 1944 | 57 | 24 |
| Operation Rheinübung — the Bismarck chase | 18–28 May 1941 | 23 | 13 |
| Operation Ten-Go — the last sortie of Yamato (skeleton) | 5–7 Apr 1945 | 1 | 0 |

## Features

- Minute-resolution timeline with playback from 10 min/s to 1 day/s; auto-slows around key events
- Ships drawn by class (battleship / carrier / cruiser / destroyer / submarine glyphs), coloured by task force, with formation flags (48-star, IJN ensign, White Ensign, Kriegsmarine)
- Sea routing around coastlines (Natural Earth 1:10m, A* on a 2–3 km grid), pre-computed at build time — nothing to download at runtime
- Carrier and land-based air strikes flying out, attacking and returning in formation; torpedo runs; gun tracers; sinking flashes
- Day/night terminator computed from the actual date and time
- Bases, airfields and headquarters with the controlling force's insignia; control changes over time
- Event timeline with losses highlighted, running casualty counter, commander cards, Wikipedia links
- Documented vs reconstructed positions distinguished (solid vs dotted routes, popup confidence note)
- Two-level timeline: the whole war at sea (1939–45) with every campaign as a block, plus the minute-resolution battle slider
- Cross-campaign ship registry — a ship's popup links to her other campaigns and gives her eventual fate
- Follow-a-ship, search, keyboard shortcuts, four UI themes (modern / wartime chart × light / dark)

Deep links: `https://bread40k.github.io/fleetview/#s=bismarck&t=1941-05-27T10:30`

## Running it

The site is published with GitHub Pages from the `main` branch — every commit goes live within a minute.

Scenario data is fetched on demand, so to run it locally serve the folder over HTTP rather than opening the file directly (browsers block `fetch()` from `file://`):

```
python3 -m http.server 8000      # or: npx serve
open http://localhost:8000/#s=leyte&t=1944-10-25T08:30
```

Runtime dependencies (loaded from CDNs, none installed):

- [Leaflet](https://leafletjs.com/) 1.9 (BSD-2)
- Esri World Ocean basemap tiles (attribution required)

## Data

```
data/
  index.json             campaign list (id, title, span, theatre, counts) + the war window — loaded first
  ships.json             cross-campaign ship registry: name, nation, class, wiki, fate, appearances
  scenarios/<id>.json    one self-contained campaign, loaded when selected
```

A scenario file is a plain JSON object:

```
id, title, subtitle, base:[year, monthIndex], start, end, tz, utcOffset, defaultTime, view, scenes, keyShips, footnote
forces       { forceId: { name, color, nation } }
routes       named base tracks: [ 'DD HH:MM', lat, lon, note?, 'S'|'R'? ]
ships        [ { id, name, force, type, route, until?, extra?, sunk?, sunkBy?, lost?, wiki?, ref? } ]
strikes      [ { id, name, nation, from:{route}|{lat,lon}, target:{ship}|{lat,lon}, launch, arrive, leave, recover, count, land?, oneway?, recoverAt?, note } ]
torpedoes, engagements (gun targets), events, ports (bases / airfields / HQ), rescues, commanders, groups
routing      { res, bbox, margin, source, bakedAt, ships:{ shipId:{ hash, snap, via } } }   ← written by the baker, don't edit by hand
```

Times are `'DD HH:MM'` in the scenario's zone time (`base` gives the year and month; Tokyo UTC+9 for Leyte, ~UTC+2 for the Bismarck chase). A ship follows its `route` until `until`, then its own `extra` track. Positions of battles and sinkings are taken from published records; transit legs between documented fixes are reconstructions and are drawn dotted — mark a waypoint `'S'` (sourced) or `'R'` (reconstructed) to override the default (a note ⇒ sourced).

`ships.json` is keyed by ship id (or a ship's `ref`, for two different ships that share an id across campaigns). A scenario ship inherits `name`, `type` and `wiki` from the registry when it doesn't set them; `appearances` are regenerated from the scenario files, everything else you add by hand is kept.

### Building

The site itself is static; the build only prepares the data and assembles `index.html`. Node ≥ 18, no packages.

```
node tools/build-data.mjs           # validate scenarios → data/index.json + data/ships.json
node tools/bake-routes.mjs [id]     # bake sea routing into the scenario JSON (downloads the coastline once, ~800 KB, cached in tools/cache/)
bash tools/build.sh                 # the above + assemble index.html + smoke test
```

Routing records are keyed by a hash of each ship's waypoints: if you edit a track and don't re-bake, that ship simply sails straight legs (with a console warning) rather than showing a stale detour.

### Sources

- Samuel Eliot Morison, *History of United States Naval Operations in World War II*, vols. X and XII
- Anthony Tully, *Battle of Surigao Strait*; combinedfleet.com Tabular Records of Movement
- Dictionary of American Naval Fighting Ships (DANFS); Naval History and Heritage Command H-Grams
- Ludovic Kennedy, *Pursuit*; Iain Ballantyne, *Killing the Bismarck*; naval-history.net
- Wikipedia articles for individual ships (linked from each ship's popup)

### Contributing

Corrections and new scenarios are very welcome — open an issue, or edit `data/scenarios/<id>.json` (a new campaign is a new file; `tools/build-data.mjs` picks it up and validates it) and send a pull request. When adding waypoints please note your source, and mark documented fixes with a fifth element `'S'` (or `'R'` for reconstructed) so the confidence display stays honest.

## Status

Two campaigns so far; the goal is the whole war at sea, 1939–45. Phase 1 (data in `data/*.json`, ship registry, war / battle timeline, baked routing) is done. Next: an ingestion pipeline for TROM / naval-history.net / DANFS sources, then battle packs — Midway, Pearl Harbor, Java Sea, Coral Sea, Matapan, River Plate, Philippine Sea, Guadalcanal, PQ 17, Ten-Go.

## Licence

- **Code:** MIT — see `LICENSE`
- **Curated data (routes, events, notes):** [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — see `LICENSE-DATA.md`
- Basemap © Esri and contributors; coastlines Natural Earth 1:10m via [world-atlas](https://github.com/topojson/world-atlas) (public domain), used at build time only; flags and insignia drawn for this project

This is a non-commercial history project. It carries no advertising and collects no data.
