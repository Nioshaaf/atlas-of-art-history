# Atlas of Art History

Art doesn't drift. It is commissioned, funded, banned, looted and exiled — and every glow on this map sits inside somebody's empire, a generation after somebody's war.

An interactive atlas of **323 art movements**, **133 historical ruptures** and **69 empires**, from 3000 BCE to 2026, all driven by a single timeline.

**[→ Open the atlas](https://nioshaaf.github.io/atlas-of-art-history/)** · one HTML file, no build step, no dependencies

---

## What it does

Scrub the timeline or press play, and three layers move together on a Natural Earth world map:

| Layer | What you see |
|---|---|
| **Empires** | Tinted territory with borders that shift as each state expands and contracts, drawn phase by phase |
| **Art movements** | Glows that brighten from a tradition's founding to its peak, then dim as it fades |
| **Events** | Expanding rings for wars, plagues, conquests and revolutions, each with a line on what it did to art |

Below the map, a centred streamgraph shows each medium's share of global activity across the whole span — the *becoming popular, then less popular* view.

Four media are tracked: **painting**, **sculpture**, **photography**, and **objects & craft**.

## Interaction

- **Timeline** — drag the scrubber, press play, or step with `←` / `→` (`⇧` for ×10)
- **Click anything** — a hotspot, an event ring, a tick on the timeline — for a card with key works and a source link
- **Filter** by medium; toggle the empire, event and label layers
- **Search** movements and events by name
- **Zoom and pan** the map with scroll and drag
- **Jump to** presets: the Parthenon, the Black Death, Leonardo, the invention of photography, the New York School
- **Data** opens the full sourced table of every record

## Design notes

**Time is piecewise, not linear.** A straight 5,000-year axis buries everything after 1400. The `BREAKS` table maps years to a 0–1 position with progressively more room for recent centuries; playback steps through *that* space so the sweep feels even. The era band along the top keeps you oriented.

**The palette was computed, not chosen.** The four medium hues (`#da7306` `#15aa8f` `#457cfd` `#c400aa`) came out of a search over OKLCH space, validated against an all-pairs colour-vision-deficiency gate on the `#0e0e12` surface: worst CVD ΔE 12.8, worst normal-vision ΔE 23.5, all four ≥ 3:1 contrast. Tritan separation is 6.2, which is why **shape encoding is mandatory** — circle, triangle, square and diamond carry the medium alongside colour. Don't drop the glyphs.

**Empire colours are normalised.** Source hues are re-stepped to OKLCH L 0.68, and empires that coexist in time are pushed at least 34° apart in hue so no two neighbours read the same.

**Co-located movements are dodged** along a golden-angle spiral — otherwise Paris, Florence and Kyoto collapse into one bright smear.

**Labels share one occupancy list** across movements, events and empires, with fallback anchor positions, so nothing overlaps.

## Data

| File | Records | Fields |
|---|---|---|
| `data/movements.json` | 323 | `id` `name` `medium` `region` `lat` `lon` `s`/`p`/`e` (start/peak/end) `i` (intensity 1–5) `d` (blurb) `w` (key works) `src` |
| `data/events.json` | 133 | `id` `name` `t` (type) `s`/`e` `lat` `lon` `m` (magnitude 1–5) `d` `a` (effect on art) `src` |
| `data/empires.json` | 69 | `id` `name` `start` `end` `color` `phases[{year, iso[]}]` |

The same data is embedded in `index.html`, so the page runs standalone; the JSON files are there for reuse.

Records were researched against Wikipedia, the Met's Heilbrunn Timeline of Art History, Britannica, Tate, MoMA, Smarthistory and World History Encyclopedia. **Every record carries a source URL**, surfaced in the app's Data table.

## Accuracy and limits

Read this before citing anything here.

- **Dates are conventional scholarly ranges**, not claims. Movements rarely have crisp boundaries; the start/peak/end triplet is a modelling convenience.
- **Empire extents are visual approximations.** Each phase is drawn by filling the *modern countries* a state substantially controlled. Good enough to watch the Mongols sweep across Eurasia or the Ottomans recede; not a boundary survey.
- **Verification was partial.** Automated checks found no ordering, future-date or missing-field anomalies, and every coordinate was tested against land geometry (three southern-hemisphere sign errors were caught and fixed). A manual fact-check of a random 31-record sample found all coordinates correct, all 10 sampled events correct, and corrected 4 movement date boundaries. The remaining records rest on the research pass alone.
- **Coverage is uneven.** Photography has 24 entries against painting's 153. Pre-1500 empire coverage for Africa, the Americas and Southeast Asia is thinner than it should be.

Corrections are welcome — open an issue or a PR against the JSON.

## Running it

Clone and open `index.html` in a browser. That's the whole thing — no server, no npm install, no network access required at runtime. The only outbound links are the citation URLs, and nothing loads until you click one.

To publish it, any static host works. For GitHub Pages: Settings → Pages → deploy from `main` / root.

## Credits

Coastline geometry derives from [world-atlas](https://github.com/topojson/world-atlas) (ISC, © Michael Bostock), built from [Natural Earth](https://www.naturalearthdata.com/) public-domain data, decoded and simplified to 0.25° for this project. See [`NOTICE`](NOTICE).

Licensed under the [MIT License](LICENSE).
