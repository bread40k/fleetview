# Changelog

## v2.0 — 2026-09-08

**Architecture (Phase 1)**
- Scenario data moved out of `index.html` into `data/scenarios/<id>.json`, loaded on demand — only the selected campaign is fetched. `index.html` shrinks from 190 KB to ~105 KB and no longer changes when data does.
- `data/index.json` lists the campaigns (span, theatre, counts) and the war-at-sea window; `data/ships.json` is a cross-campaign ship registry (name, nation, class, Wikipedia link, fate, every appearance). Scenario ships inherit name / type / wiki from the registry when not set locally; popups link to a ship's other campaigns.
- Two-level timeline: a war bar (Sep 1939 – Sep 1945) above the battle slider shows every campaign as a block; click one to open it, click inside the current block to jump within the battle. Position marker tracks the clock.
- Sea routing is now baked at build time (`tools/bake-routes.mjs`, same A* on Natural Earth 1:10m) into each scenario's `routing` block; the browser downloads no coastline data. Routing records are keyed by a hash of the ship's waypoints, so edits made after a bake fall back to straight legs (with a console warning) instead of drawing stale detours. The "Sea routing" toggle still works.
- Build pipeline: `tools/build-data.mjs` validates every scenario (ids, time order, leg speeds, cross-references) and writes the index and registry; `tools/build.sh` assembles the site; the smoke test now runs against the real JSON via a stubbed `fetch()`.
- Because data is fetched, the site must be served over HTTP when run locally (`python3 -m http.server`); opening `index.html` from `file://` shows an explanatory message.

**Compatibility**
- Deep links (`#s=…&t=…`), scenes, follow, search, themes, mobile sheets and all v1.3 features unchanged. The `'DD HH:MM'` time convention and the waypoint / ship / strike schema are the same in JSON as they were in JS.

## v1.3 — 2026-09-08

**Rescue operations**
- New `rescues` data type: lifebuoy marker over the rescuing ship, dotted line to the wreck, label with men saved; click for details. 15 operations across both campaigns, plus 🛟 timeline events.
- New ships: Shimakaze, Kiyoshimo, Nowaki, Fujinami (Leyte); HMS Electra, HMS Tartar (Bismarck).
- Casualty figures for Chōkai and Chikuma now reflect men lost at the sinking; their rescued crews are counted when Fujinami and Nowaki were lost.

**Playback**
- "Slow down for key events" toggle (renamed from Auto-slow). Slow-down now triggers only on key events: every ship loss plus the opening of each action. Key events are bold in the timeline, with a ★ on non-loss ones.

**Casualty counter**
- Now labelled with Losses / Rescued columns per nation; a cumulative Rescued figure rises during each rescue.
- Numbers tick toward new values instead of jumping.
- Fixed the counter being squeezed by the time bar and overlapping its columns.

**Other**
- Version number shown in the header (replaces "Prototype").

## v1.2 — 2026-09-08
- Mobile: page locked against overscroll; bottom sheets scroll as a whole so the campaign selector, search and options are always reachable.

## v1.1 — 2026-09-08
- Mobile layout: full-screen map, top bar with Fleets / Timeline bottom sheets, compact time bar, safe-area padding.
- Esri attribution repositioned above the time bar on all layouts.

## v1.0 — 2026-09-08
- First public release on GitHub Pages: Battle of Leyte Gulf and Operation Rheinübung.
