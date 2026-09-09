# FleetView

**An interactive, time-scrubbable map of WW2 naval battles.**

**▶ Live site: https://bread40k.github.io/fleetview/**

Drag the timeline and watch fleets move, aircraft strike, guns fire and ships go down — with every position, sortie and loss placed in time and space. Built for people who read Morison and Tully for fun and wondered why nobody had drawn it.

Currently included:

| Campaign | Dates | Ships | Air ops |
|---|---|---|---|
| Battle of the River Plate | 1–20 Dec 1939 | 9 | 2 |
| The Battles of Narvik | 7–14 Apr 1940 | 36 | 4 |
| Battle of Cape Matapan | 26 Mar – 1 Apr 1941 | 33 | 9 |
| Operation Rheinübung — the Bismarck chase | 18–28 May 1941 | 25 | 13 |
| The Royal Navy at Crete | 20 May – 1 Jun 1941 | 41 | 16 |
| The Attack on Pearl Harbor | 25 Nov – 8 Dec 1941 | 51 | 5 |
| The Channel Dash — Operation Cerberus | 11–13 Feb 1942 | 17 | 5 |
| The Doolittle Raid | 2–25 Apr 1942 | 19 | 5 |
| Battle of the Coral Sea | 1–12 May 1942 | 46 | 12 |
| Battle of Midway (with the Aleutians diversion) | 25 May – 7 Jun 1942 | 70 | 31 |
| Convoy PQ 17 | 27 Jun – 13 Jul 1942 | 74 | 8 |
| Battle of the North Cape | 22–27 Dec 1943 | 22 | 1 |
| Operation Tungsten — the Fleet Air Arm strikes Tirpitz | 27 Mar – 7 Apr 1944 | 33 | 5 |
| Battle of Leyte Gulf | 17–28 Oct 1944 | 61 | 24 |
| Operation Ten-Go — the last sortie of Yamato | 5–8 Apr 1945 | 30 | 11 |

## Features

- Minute-resolution timeline with playback from 10 min/s to 1 day/s; auto-slows around key events
- Ships drawn by class (battleship / carrier / cruiser / destroyer / submarine glyphs), coloured by task force, with formation flags (48-star, IJN ensign, White Ensign, Kriegsmarine ensign drawn with an Iron Cross in place of the party emblem, Regia Marina, Norwegian and Soviet naval ensigns); flags of nearby formations merge into one at low zoom
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
  milestones.json        non-naval reference dates shown as clickable dots under the war bar (embedded into index.json)
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

Times are `'DD HH:MM'` in the scenario's zone time (`base` gives the year and month; Tokyo UTC+9 for Leyte and Ten-Go, ~UTC+2 for the Bismarck chase, Midway local UTC−12 for Midway), or `'YYYY-MM-DD HH:MM'` when a campaign spans two months. A scenario that straddles the 180th meridian sets `view.dateline: true` and writes its longitudes continuously (177°W as 183), so tracks never wrap; the app normalises them for display. A ship follows its `route` until `until`, then its own `extra` track. Positions of battles and sinkings are taken from published records; transit legs between documented fixes are reconstructions and are drawn dotted — mark a waypoint `'S'` (sourced) or `'R'` (reconstructed) to override the default (a note ⇒ sourced).

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

- Samuel Eliot Morison, *History of United States Naval Operations in World War II*, vols. IV, X, XII and XIV
- Jonathan Parshall & Anthony Tully, *Shattered Sword*; Nagumo's action report (*The Japanese Story of the Battle of Midway*, ONI 1947); CINCPAC, Enterprise, Hornet and Yorktown action reports; ONI Combat Narrative *The Battle of Midway*
- CTF 58 action report (Ten-Go); NHHC H-Gram 044; Tameichi Hara, *Japanese Destroyer Captain*
- London Gazette despatches: Harwood (River Plate), Warburton-Lee / Whitworth (Narvik), Cunningham (Matapan, Crete), Fraser (North Cape); Bucknill enquiry extracts (Channel Dash)
- Pearl Harbor: Nagumo's operation orders (Japanese Monograph 97), combinedfleet.com TROMs, NHHC action reports; Coral Sea: CTF 17, Lexington and Yorktown action reports; Doolittle: Hornet, Enterprise and Doolittle's own reports (ibiblio HyperWar); Tungsten: Admiralty War Diary (naval-history.net), Battle Summary No. 27
- combinedfleet.com, scharnhorst-class.dk, uboat.net (PQ 17 losses), warsailors.com, the Narvik dive-site surveys (dykkepedia.com), Italian and German Wikipedia for the Regia Marina and Kriegsmarine side
- Anthony Tully, *Battle of Surigao Strait*; combinedfleet.com Tabular Records of Movement
- Dictionary of American Naval Fighting Ships (DANFS); Naval History and Heritage Command H-Grams
- Ludovic Kennedy, *Pursuit*; Iain Ballantyne, *Killing the Bismarck*; naval-history.net
- Wikipedia articles for individual ships (linked from each ship's popup)

### Contributing

Corrections and new scenarios are very welcome — open an issue, or edit `data/scenarios/<id>.json` (a new campaign is a new file; `tools/build-data.mjs` picks it up and validates it) and send a pull request. When adding waypoints please note your source, and mark documented fixes with a fifth element `'S'` (or `'R'` for reconstructed) so the confidence display stays honest.

## Status

Fifteen campaigns so far; the goal is the whole war at sea, 1939–45. Phase 1 (data in `data/*.json`, ship registry, war / battle timeline, baked routing) and Phase 2 (the ingestion pipeline) are done; Phase 3 battle packs are under way — next Java Sea, Force Z, Guadalcanal, Philippine Sea, Pedestal, Taranto, Truk.

## Licence

- **Code:** MIT — see `LICENSE`
- **Curated data (routes, events, notes):** [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — see `LICENSE-DATA.md`
- Basemap © Esri and contributors; coastlines Natural Earth 1:10m via [world-atlas](https://github.com/topojson/world-atlas) (public domain), used at build time only; flags and insignia drawn for this project

This is a non-commercial history project. It carries no advertising and collects no data.
