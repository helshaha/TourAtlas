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

<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.
<!-- LOVABLE:END -->
