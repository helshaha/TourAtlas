# TourAtlas — tourism that works offline

TourAtlas is an offline-first workspace for local tourism operators. A visitor speaks or writes in their own language, the operator understands the request, approves a reply in their own words, and everything keeps working when the signal disappears.

## Watch

| Video | What it covers | Link |
| --- | --- | --- |
| Team introduction | Who is behind TourAtlas and why it exists | https://youtu.be/oFYcHAJsyqc |
| Product description | The visitor-to-operator journey end to end | https://youtu.be/vU0QsG1MOB4 |
| Technical depth | Offline models, maps, speech, sync and evidence | https://youtu.be/CNfpmA17Ng4 |

## What it does

- **Multi-country operator packs** — Gambia, Jordan, Ukraine and any place an operator adds themselves, each with its own local language, facts, enquiries, feedback, heritage notes and queued actions. Switching region never mixes another operator's records.
- **Voice in and out** — hold-to-speak capture, online transcription through the app's own server endpoint, browser speech as the offline fallback, and spoken replies where the device supports them.
- **Translation with a human in the loop** — visitor messages are translated for understanding; the reply the visitor actually receives is written and approved by the operator.
- **Local intent and case building** — dates, times, group size, budget, meeting points and availability are read out of the conversation and accumulate across turns, including relative phrasing such as "after tomorrow" or "10 am to 10 pm".
- **Maps** — an interactive 3D explorer for orientation, an online map for live search, and offline map packs (prepared areas plus operator-saved custom areas) that reopen with the network switched off.
- **Heritage protection mode** — private, operator-only notes on historical places, with an explicit opt-in before anything leaves the device.
- **Feedback and weekly insights** — visitor reviews are grouped into themes locally, with an evidence-based suggestion and a spoken summary.
- **Store-and-forward outbox** — approved replies are held on the device and handed to the phone's messaging app, or sent through a connected SMS account once one is linked. Delivery is only ever shown as the provider reports it.
- **Cross-device sync** — opt-in, device-first, per-record rows scoped to the signed-in operator; heritage notes stay private unless the operator says otherwise.
- **Accessibility** — large-text mode, voice-only mode, bottom navigation with swipes, haptics, and an ambient sound toggle.

## Connection status, honestly

The header shows what the browser can actually observe — online, offline, or estimated unstable — kept separate from the operator's typical-connection preference, which is a choice, not a measurement.

Every capability carries an explicit status instead of a claim: `VERIFIED`, `CONNECTED`, `LOCAL ONLY`, `DEVICE DEPENDENT`, `NOT IMPLEMENTED YET`, `NOT MEASURED`, `NOT CONNECTED`. A feature only moves to `VERIFIED` after a real test passes on the device — for example, an offline map is verified only after a recorded disconnect test (airplane mode, reopen, pan, zoom), and on-device models only after a run with the network off. The Evidence screen reports what was measured here, and says "Not measured" when it wasn't.

## Screens

| Route | Purpose |
| --- | --- |
| `/` | Home: today's enquiries, approvals, collected stories, weekly insights |
| `/voice` | Hear a visitor, capture speech, prepare a reply |
| `/inbox` | Ongoing conversations, case details, outbox and SMS handoff |
| `/map` | 3D explorer, online search, offline packs and custom saved areas |
| `/heritage` | Private notes on historical places |
| `/insights` | Feedback themes, evidence, suggestions |
| `/evidence` | Capability matrix and measured numbers |
| `/experience` | The operator's own tourism pack |
| `/profile` | Setup, offline models, sync, accessibility |
| `/discoverability` | Checks on how findable the offering is |

## Using the app — step-by-step

### The Map screen: what you see

- The map on top is an online raster map (OpenStreetMap tiles). It requires an active internet connection to stream map tiles.
- When a custom pack (e.g. "Saudi Arabia — Custom Pack") has just been created, no tourism places have been fetched from OpenStreetMap yet. That is why it says "No saved places for this area yet".
- By default the region is shown zoomed out; zoom into a city or district to work with it.

### Can I open a whole country offline?

- A whole country at once? **No.** Offline maps in TourAtlas store real vector geometries (POIs, streets, footpaths, water, and building outlines) directly inside your browser cache rather than downloading prohibited image tiles. To prevent your browser from freezing or running out of memory, custom offline captures are capped at 25 km² (a town center, archaeological site, or neighborhood).
- A specific city or site (e.g. Al-Balad in Jeddah, Hegra / Al-Ula, Diriyah in Riyadh)? **Yes.** Zoom into a 25 km² area while connected and tap "Save this area offline". TourAtlas packages all the roads, buildings, and tourism POIs into your local device cache, and you can then view, pan, and search that area completely offline.

### A. Search and zoom to a specific place

1. In the search bar at the top, type a specific city or landmark (e.g. Jeddah, Al Ula, or Riyadh) and tap Search.
2. Tap the result in the dropdown list ("View on map"). The map flies directly to that location.

### B. Discover and filter local tourism places

1. Once centered over your destination, tap "Load tourism places in view".
2. TourAtlas queries OpenStreetMap for local tourism landmarks, attractions, hotels, and heritage points.
3. Tap the category filter chips above the map (Attractions, Heritage, Stay, Food, Transport) to filter the markers and the list below.

### C. Save an area for 100% offline use

1. Zoom in on the map until you are looking at a specific district or town center (under 25 km²).
2. Tap "Save this area offline" in the OFFLINE MAP section.
3. Enter a label (for example, "Al-Balad Old Town" or "Hegra Reserve").
4. TourAtlas downloads vector paths, buildings, and POIs into browser storage.
5. Scroll down to "Maps that work without signal": your custom pack appears alongside the demo packs. Tap "Open map" to open the vector viewer — this works even in Airplane mode.
6. To earn the `VERIFIED` status, reopen the saved pack with the network off, pan and zoom once, and run "Check offline test result".

### D. Place your own tour or business listing on the map

1. Tap "Place my business" in the toolbar.
2. Click anywhere on the map where your tour start, camp, or office is located.
3. Your coordinates are pinned as the official meeting point in your pack.

### E. Switch the active workspace

1. Tap "Create a Local Tourism Pack here".
2. Enter the region details: operator language (e.g. Arabic) and visitor languages (e.g. English, French, German).
3. Tap Create pack. Conversations, voice translation, and local fact sheets across the app now align with this workspace, and each region keeps its own records separate.

### The Inbox: from visitor message to approved reply

1. Open `/inbox`. The latest conversation is selected by default, sorted by the most recent activity.
2. Read the conversation and the case details gathered from the messages: dates, times, group size, budget, availability, and meeting points. "After tomorrow" and "10 am to 10 pm" are interpreted as real dates and time ranges.
3. Hold to speak to reply by voice, or type. Uncertain language or meaning guesses are shown with a confidence warning.
4. Review the drafted reply, edit it, and approve it — no reply ever leaves the device automatically.
5. Approved replies go to the local outbox. Hand them to the phone's messaging app, or send via SMS if a connected sending account is linked; delivery is only shown as the provider reports it.

### Offline language models (Profile)

1. Open `/profile` and find the offline model downloads: OPUS-MT translation pairs (via an English pivot) and Whisper tiny for transcription, plus the optional WebGPU assistant.
2. Download the models you need while connected. Sizes and speeds are measured on your device, not quoted from a datasheet.
3. Use them offline afterwards. A capability is only marked `VERIFIED` after a run with the network off; until then it reads `NOT IMPLEMENTED YET` or `DEVICE DEPENDENT`.

### Heritage, insights and sync

1. `/heritage` — write private, operator-only notes on historical places. Nothing leaves the device unless you explicitly opt in.
2. `/insights` — visitor feedback is grouped into themes locally, with an evidence-based suggestion.
3. `/profile` → Sync — cross-device sync is opt-in and device-first: signed-in operators push and pull per-record rows; heritage notes sync only when you opt in.

## Tech stack

- TanStack Start v1 (React 19, file-based routing, server functions)
- TypeScript, Tailwind CSS v4
- Three.js / react-three-fiber for the 3D explorer, Leaflet for the online map
- transformers.js (OPUS-MT translation pairs, Whisper) and web-llm (WebGPU assistant) for optional on-device models
- Cache API for offline packs and areas; browser storage as the primary record store
- Lovable Cloud (database, auth, functions) for optional sync and connected services
- Vitest for tests, ESLint and Prettier for code quality

## Getting started

Requires Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```

Then open the printed local address. On a phone, use the same network and the machine's address, or install the app to the home screen.

## Scripts

```sh
npm run dev         # development server
npm run build       # production build
npm run preview     # serve the production build
npm test            # run the test suite
npm run lint        # ESLint
npm run format      # Prettier
```

## Notes and limits

- Offline maps come from prepared OpenStreetMap-derived GeoJSON packs and operator-saved areas, rendered without tile imagery. Public OSM tile bulk downloads are not used, in line with the tile usage policy.
- On-device models are optional downloads and depend on the device (WebGPU for the assistant, storage for the rest). Model size and speed are measured locally rather than quoted from a datasheet.
- SMS needs a connected sending account and explicit operator approval before anything is queued; the phone's own messaging app is always available as a fallback.
- Translation quality should be confirmed with a speaker of the language before publishing tourist-facing text.

> the editor, so keep the branch in a working state.
<!-- LOVABLE:END -->
