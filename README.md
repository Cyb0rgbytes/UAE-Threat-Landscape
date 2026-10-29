# درع الإمارات — UAE Cyber Threatscape v2.0

A cinematic SOC wall / briefing / threat-intel command center. **All data is simulated and illustrative.**

## Run
Open `index.html` directly (works from `file://`, fully offline), or serve the folder:
`python -m http.server 8731` → http://localhost:8731

Keys: `Ctrl/⌘ K` search & commands · `?` shortcuts sheet · `Esc` close / clear focus · `Space` pause · `F` fullscreen · `R` reset · `1–6` categories · `G` D3 globe · `O` Orbital (Three.js) · `H` holo shader · `M` alert sting · `W` presenter scenarios

## Interacting (v2.1)
- **Everything filters.** Click a matrix cell (category × severity), a kill-chain stage, an actor constellation, a sector icon, or an Emirate node (map or inset) to isolate it. Active filters appear as removable chips above the map; `R` or *Clear all* resets. Hovering any of these dims the arcs, tokens and links that don't match.
- **Timeline brush.** The replay slider sits on a 24 h stacked histogram (10-minute bins, category colours, shaded = current window). Drag or use `← →` to replay; gold ticks under the baseline are detected campaigns — click one to replay from 5 min before it. The label shows LIVE (with feed staleness), PAUSED or REPLAY.
- **Incident inspector.** Click a feed line or an arc head on the map (hover shows a tooltip) to open the slide-over: route, note, damage, attribution, kill-chain stepper, and actions (*Replay arc*, *Focus*, *Similar incidents*, *Copy JSON*). Clicking a country or a ranked row opens its dossier (inbound by category, block rate, most active groups).
- **Command palette.** `Ctrl/⌘ K` jumps to any country, category, actor group, sector, Emirate or command (modes, views, windows, scenarios, export). Bilingual matching.
- **Deep links.** Mode, window, view, filters and focus are mirrored into the URL hash (`#m=…&w=…&v=globe&c=ddos,apt&s=3&f=SAU&a=GF…`), so a view can be bookmarked or shared; it is restored on load.
- **Presenter scenarios** (`W`, hidden in Briefing): launch a campaign against the UAE, a critical ICS / DDoS / APT hit, a blocked wave at the perimeter, calm down, or change the attack rate (×0.25–×4). Every injected event is marked *simulated* in the feed. Also via `threatscape.scenario('ics')`, `threatscape.inject({...})`, `threatscape.setRate(2)`, `threatscape.inspect('SAU')`.

## Structure
- `index.html` — the app. Theme tokens in `:root`, tunables in `CONFIG`, every file path in `ASSETS`.
- `index-v1.html` — the previous version (CDN-based), kept for reference.
- `assets/video` — background plate, shield VFX, globe turntable (WebM + MP4 each)
- `assets/img` — impact bursts, mashrabiya lattice, hero (1080p), background poster
- `assets/icons` — eight sector line icons (SVG)
- `assets/vendor` — d3 7.9.0, topojson-client 3.1.0, three.js r149 (UMD), world-atlas countries-110m
- `assets/fonts` — Cairo, Inter, JetBrains Mono, Twemoji country flags

## Plugging in real data
1. `threatscape.setSimulation(false); threatscape.clear();`
2. Map each SIEM/XSOAR alert to `{ ts, src, dst, category, severity, damageUSD, blocked, note }`, plus optional `volume, dstNode, stage (1–7 or 'Exploit'), actor, sector, preventedUSD`.
3. Push batches: `threatscape.ingest(batch)`, from a `setInterval(fetch…)` poll or a WebSocket/EventSource `onmessage`.
4. Use your own actor groups: `threatscape.defineActors([{ key:'TA1', en:'…', ar:'…', color:'#hex' }])`. Unknown countries: `threatscape.addCountry(code, {…})`.
5. Thresholds for campaigns, shockwaves, arc caps and the ledger are in `CONFIG`. Asset swaps go in `ASSETS`.

## Higgsfield assets (all original, AI-generated; C2PA provenance kept in SVGs)
| Asset | Model | Credits |
|---|---|---|
| A1 background still (3 variants, #1 used) | GPT Image 2.5 | 0.75 |
| A2 background plate, 12 s loop | Kling 3.0 Pro | 18 |
| B mashrabiya lattice (2 variants) | Recraft V4.1 vector | 5 |
| C shield VFX, 4 s (2 variants, A used) | Kling 3.0 Pro | 12 |
| D impact bursts ×3 | GPT Image 2.5 | 0.75 |
| E globe turntable, 8 s | Kling 3.0 Pro | 12 |
| F hero frame drafts (3) + final, native 4K | GPT Image 2.5 | 0.75 + 4.25 |
| G sector icons ×8 | Recraft V4.1 vector | 20 |
| **Total** | | **73.5** |

No upscale or background-removal runs were needed. The hero was generated natively at 3840×2160, and black backgrounds are removed in-browser with `mix-blend-mode: screen`.
