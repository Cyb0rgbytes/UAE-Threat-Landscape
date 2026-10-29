# درع الإمارات — UAE Cyber Threatscape v2.0

A cinematic SOC wall / briefing / threat-intel command center. **All data is simulated and illustrative.**

## Run
Open `index.html` directly (works from `file://`, fully offline), or serve the folder:
`python -m http.server 8731` → http://localhost:8731

Keys: `Space` pause · `F` fullscreen · `R` reset · `1–6` categories · `G` D3 globe · `O` Orbital (Three.js) · `H` holo shader · `M` alert sting

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
