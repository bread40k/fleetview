# Changelog

## v2.8 — 2026-09-09

**Major damage** — ships can now carry `damage: [[time, hours, note]]`. A hit that mattered historically draws a smaller smoke plume that travels with the ship for the given hours (or until she sinks) and is a slow-down point for playback. 91 entries added across all fifteen campaigns: Tirpitz in Kåfjord, the four Midway carriers between their hits and their sinkings, Yorktown twice, Shōkaku, Vittorio Veneto, Warspite and Formidable off Crete, Exeter, Musashi, Bismarck's Prince of Wales hits, Nevada and the harbour at Pearl…

**Slow-down points** — "Slow down for key events" now also engages as every air strike of six or more aircraft reaches its target (Tokyo, Kåfjord, Battleship Row, Midway's carriers, Shōhō) and at every major-damage moment, whether or not a timeline entry exists.

**Hand-painted tracks** — `routing.manual: [ids]` in a scenario tells the route baker to leave those ships' or routes' waypoints exactly as written, so a track drawn by hand through a harbour or fjord is never re-routed. Pearl Harbor's channel is the first: Nevada's run down the channel, the midget submarine's approach, and the carriers' passage in and out of the harbour entrance are now painted point by point.

## v2.7.2 — 2026-09-09

- **Smoke plumes** — a wreck now smokes for ten hours of battle time after sinking, the plume thinning as it goes (drawn from zoom 6 up, in the same layer as the sinking flash).
- The "Slowed to …" banner now states the actual rate (3 min/s at normal speeds, matching the playback engine) instead of a fixed "10 min/s".

## v2.7.1 — 2026-09-09

- **Slower playback**: 1 min/s and 3 min/s added to the speed menu. A scenario can set `defaultSpeed` (ms of battle time per second); Pearl Harbor now opens at 3 min/s — the whole attack lasted under two hours. "Slow down for key events" now drops to 3 min/s (was 10) and also engages at 10 min/s.
- **Satellite detail when zoomed in**: from zoom 11 Esri World Imagery is laid over the ocean chart, which has no detail beyond zoom 10 — Battleship Row, Ofotfjord and Kåfjord now resolve. Present-day imagery; a panel toggle turns it off.

## v2.7 — 2026-09-09

**Guided camera** — a 🎬 option in the panel. The camera picks its own subject and hands over as the battle unfolds: the biggest carrier strike in the air (land-based raids second), otherwise the key ship with the next documented moment — Hornet across the Pacific, then Doolittle's B-25s to Tokyo, then Nagumo's carriers. Switching flies the map to the new subject; Esc, dragging the map or the ✕ on the chip stops it. Playback starts automatically.

**Follow air groups** — clicking an aircraft formation now offers ◎ Follow; the view tracks the strike until it recovers, then releases. The follow chip shows ✈ for air groups.

**Popup controls during playback** — the ship popup is now patched in place each frame instead of being rebuilt, so Follow and Wikipedia can be clicked while the clock is running.

Smoke test drives the guided camera through every campaign and checks strike following.

## v2.6.1 — 2026-09-09

**Campaign selector** — each entry now begins with its month and year (`Dec 1939 · Battle of the River Plate`), taken from the campaign's default time, so the dates line up down the list. The list was already in chronological order.

## v2.6 — 2026-09-09

**Four new campaigns**
- **The Attack on Pearl Harbor** (25 Nov – 8 Dec 1941): the Kido Butai's northern route from Hitokappu Bay (reconstructed from its operation orders), the two waves, the midget submarines and Ward's first shot, Battleship Row berth by berth with Nevada's run, Enterprise's scouts flying into the raid, Lexington and Indianapolis at sea. Second dateline campaign (continuous longitudes). 51 ships, 8 torpedo hits.
- **Battle of the Coral Sea** (1–12 May 1942): Point Buttercup, the Tulagi strikes, the two forces 70 miles apart in the dark, Neosho and Sims, Shōhō ('Scratch one flattop'), Crace off Jomard Passage, the dusk strike, the 8 May exchange and Lexington's end, Neosho found four days later. 46 ships, 12 air operations.
- **The Doolittle Raid** (2–25 Apr 1942): Hornet from Alameda, Enterprise from Pearl, the rendezvous at 38°N 180°, Nitto Maru, the launch 650 miles out, the sixteen B-25s drawn as one flight to Tokyo and on to Chuchow (and York's to Vladivostok), Nagumo's futile chase. Third dateline campaign.
- **Operation Tungsten** (27 Mar – 7 Apr 1944): Forces 1 and 2, convoy JW 58 with its three U-boat kills (positions from uboat.net), the two Barracuda strikes on Tirpitz in Kåfjord, Duke of York's detachment. The flying-off position is derived (120 miles NW of Kåfjord — no fix published).

**Engine** — a ship sunk with no known death toll no longer breaks the popup (`lost: null` guarded). Smoke test: 18 runs.

**Registry** — 442 ships. Enterprise now in four campaigns (Pearl Harbor, Doolittle, Midway, Leyte); Akagi, Zuikaku and Shōkaku in three; Yorktown links Coral Sea and Midway; Hornet CV-8 Doolittle and Midway; West Virginia and California carry their raising and return to Surigao Strait in their fates. Some sixty hand-edited fates added.

## v2.5 — 2026-09-09

**Seven new campaigns — the war in European waters**
- **Battle of the River Plate** (1–20 Dec 1939): Graf Spee's last three victims, Harwood's concentration and the action of 13 December from his despatch (Zone +2), the chase to Montevideo, Cumberland's dash from the Falklands, the scuttling. 9 ships, 20 events.
- **The Battles of Narvik** (7–14 Apr 1940): Glowworm and Hipper, Renown off Lofoten, the seizure of Narvik and the sinking of Eidsvold and Norge, Warburton-Lee's dawn attack and retreat, Warspite's day — all ten German destroyers, U-64 and the Norwegian coast-defence ships with their wreck positions from the dive surveys. 36 ships, 13 torpedo attacks, 29 events. Norwegian naval ensign added.
- **Battle of Cape Matapan** (26 Mar – 1 Apr 1941): Iachino's four divisions, Pridham-Wippell's cruisers, Formidable's three strikes, the night action at 3,800 yards, Pola's end and the Gradisca rescue. 33 ships. Regia Marina ensign and roundel added.
- **The Royal Navy at Crete** (20 May – 1 Jun 1941): the Lupo and Sagittario convoys, the losses of 22–23 May, Formidable's Scarpanto strike, the Heraklion run and four nights off Sphakia, Calcutta's loss — nine ships sunk, 16 air operations, VIII Fliegerkorps' airfields as bases.
- **The Channel Dash** (11–13 Feb 1942): Brest to the Elbe hour by hour, the failed patrols, Esmonde's Swordfish, the MTBs and Pizey's destroyers, three mine strikes; Donnerkeil as an air operation. Every position reconstructed — no source records a fix.
- **Convoy PQ 17** (27 Jun – 13 Jul 1942): all 35 merchant ships as individual tracks (24 sinkings from uboat.net and the shipwreck lists, 11 survivors into Archangel or the Novaya Zemlya bays), the escort, Hamilton's cruisers, Tovey's Home Fleet, Rösselsprung with Tirpitz, Scheer and the grounded Lützow, K-21's attack, nine U-boats. Soviet naval ensign added. 74 ships.
- **Battle of the North Cape** (22–27 Dec 1943): Fraser's despatch positions for every force at 04:00, Belfast's radar fixes, Scharnhorst's two brushes with Burnett and her end — 21 torpedo salvoes. 22 ships.

**Engine**
- Nations: Regia Marina (RM), Royal Norwegian Navy (RNN) and Soviet Navy (VMF) with ensigns, airfield roundels and casualty-counter columns.
- Merchant / tanker / rescue-ship glyph (smaller, blunt-bowed); MTBs and coast-defence ships drawn small.
- **Coastline fix in the route baker:** world-atlas draws rings that cross the antimeridian (Chukotka, Wrangel Island) as single rings with a seam edge spanning the world; the scanline fill read those edges as coastline and flooded the Norwegian Sea between 66° and 72°N with phantom land, driving every Narvik and PQ 17 waypoint "ashore". Rings are now unwrapped before rasterising. `routing.snap: false` lets a scenario keep its documented positions where the 1:10m coastline cannot resolve a fjord (Narvik).
- Smoke test boots all eleven campaigns (14 runs).

**Registry** — 351 ships; Warspite, Ajax and Hotspur now link three campaigns each, Scharnhorst appears in Narvik, the Channel Dash and North Cape; hand-edited fates added for some forty ships.

## v2.4 — 2026-09-08

**Flag consolidation** — formation flags of the same nation whose anchors fall within ~46 px of each other on screen are drawn as a single flag: the largest group's name on top, the others listed beneath it (up to three, then "+n more"). Zooming in separates them again. Clicking a merged flag offers a pick-list of the formations (with their commanders) instead of one commander card. Cures the label pile-up in the Bismarck chase when Home Fleet, Wake-Walker, Vian and Rodney converge.

**Kriegsmarine ensign** — redrawn with an Iron Cross on the central disc (in the manner of the 1933–35 war ensign) plus the Iron Cross canton; the party emblem is deliberately not shown.

## v2.3 — 2026-09-08

**War-bar milestones** — 26 non-naval reference dates (Poland, Barbarossa, Stalingrad, D-Day, VE Day, Hiroshima, Nagasaki, VJ Day, Tokyo Bay …) drawn as small dots under the war bar; click one for the date and text (hover shows a tooltip too). Edited in `data/milestones.json`, embedded into `index.json` by the build. Naval events are deliberately excluded — they belong to campaign packs. Hidden on mobile.

## v2.2 — 2026-09-08

**New campaign: Battle of Midway (25 May – 7 June 1942)** — 70 ships in eleven forces, from the Kido Butai's sortie from Hashirajima and Kakuta's from Ōminato to the Aleutian landings: Nagumo's approach (his one pre-battle fix, 37°01′N 171°07′E), the four carriers' hits and sinking positions from the TROMs and Nagumo's report, the US carriers' positions from the Enterprise / Yorktown action reports, Point Luck, the transport convoy, Cruiser Division 7's collision and Mikuma's end, I-168's shelling of Midway and attack on Yorktown, Nautilus and Tambor, Theobald's TF 8 and the Dutch Harbor raids. 31 air operations (Tomonaga's strike, Midway's six piecemeal attacks, VT-8, McClusky and Leslie, the Hiryū strikes, the cruiser strikes of 6 June, both Dutch Harbor raids), 11 torpedo attacks, 8 gunnery periods, 51 events, 19 bases and HQs (Kiska and Attu change hands), 7 rescues, 13 commander cards. Midway local time (UTC−12).

**Operation Ten-Go completed** — Yahagi and the eight destroyers with their fates (Asashimo lost alone with all hands, Isokaze and Kasumi scuttled, Suzutsuki home stern-first), Task Force 58's twelve carriers and the three strike waves from the CTF 58 report, Deyo's blocking force, Threadfin and Hackleback, Kikusui No. 1, the Hancock kamikaze, 9 torpedo attacks, 6 rescues, five commander cards, Hiyoshi / Kanoya / Guam HQs. Yamato's loss corrected to 3,055 (was her complement). Events rewritten.

**Engine**
- Scenarios can straddle the 180th meridian: `view.dateline: true` turns off Leaflet's world-copy jump, longitudes are written continuously (177°W → 183°) and normalised for display; the day/night terminator now spans three world copies.
- Bases can be captured by either side: `capturedBy` on a port (Kiska, Attu → IJN); toast and label wording follow.
- Smoke test boots every campaign (7 runs) and checks scenes and pre-sortie ships; test times are relative to the campaign window.

**Registry** — 156 ships; Yamato now in three campaigns, Isokaze and Hamakaze in two (fates from Ten-Go), Mogami / Kumano / Suzuya / Nowaki / Abukuma / Enterprise link Midway and Leyte. Hornet CV-8 (`hornet_cv8`) and Yorktown CV-10 (`yorktown_cv10`) are kept apart from their namesakes with `ref`.

## v2.1 — 2026-09-08

**New campaign: Operation Ten-Go (5–7 April 1945)** — skeleton generated by the new ingestion pipeline from the combinedfleet.com TROM of Yamato: her track from Mitajiri through Bungo Suido to the sinking at 30-22N 128-04E, 16 timed events from the air attack, four ports, Ito's commander card. Escorts, TF 58 strikes and US positions to follow.

**Phase 2 — ingestion pipeline** (`tools/ingest.mjs`, not part of the site): parses combinedfleet.com Tabular Records of Movement, naval-history.net service histories, DANFS entries and uboat.net patrol pages into ship records and scenario fragments, with a port-name geocoder and per-waypoint `'S'`/`'R'` confidence flags. Tested on Yamato, HMS Rodney, USS Enterprise and U-556. Documented in `tools/README.md`.

**Registry** — Yamato now appears in two campaigns; her fate reads "sunk 7 Apr 1945 — Operation Ten-Go".

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
