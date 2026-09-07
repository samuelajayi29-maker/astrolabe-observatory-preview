# Astrolabe Observatory — Redesign Preview

Phase 1 shell of the AI Access Observatory redesign, built as an Astrolabe Data product.

**Preview:** https://samuelajayi29-maker.github.io/astrolabe-observatory-preview/

## What this is

The current Observatory (https://samuelajayi29-maker.github.io/ai-access-observatory/) is a static four-page site whose tracker data lives inside HTML markup, updated daily by a cron pipeline. This repo is the redesign: same daily data, restructured.

Core change: **data out of markup.** The live feed is rendered from `data/items.json` by `app.js`, so caps, counts, ordering and the See-more toggle are computed, never string-edited. `data/items.json` holds the migrated feed (242 unique items after dedupe, as of 2026-09-08).

## Structure

| File | Purpose |
|---|---|
| `index.html` | Product homepage: hero, dimensions, live tracker (JSON-driven), metrics, audience, weekly band |
| `style.css` | Shared stylesheet (Astrolabe Data identity, Instrument Sans) |
| `app.js` | Fetches `data/items.json`, sorts newest-first, renders the three feeds, powers accessible See-more |
| `data/items.json` | The dataset: `{updated, buckets: {jobs, access, infra: {label, items[]}}}` |
| `jobs.html` / `access.html` / `infra.html` | Dimension pages (placeholder: editorial content lands in the next phase) |
| `methodology.html` | Sourcing and independence rules |
| `favicon.svg` | Ring-and-dot mark |

## Data model

Each item: `{t: title, u: url, s: source, d: date label, dot: category}`. Dates are parsed year-aware (a "Dec" entry seen in January reads as last year) and the feed sorts newest first. Entries over a year old should be archived at rollover.

## Status

- [x] Shell (index, styles, renderer)
- [x] Data migration and dedupe (242 items)
- [x] Placeholder dimension + methodology pages
- [ ] Phase 2: updater writes `items.json` + CSV in single-commit pushes
- [x] Phase 3: deep-dive essays migrated into the dimension pages (each above its live feed)
- [ ] Newsletter form wired to a provider
- [ ] Swap live after QA; current repo tagged for rollback

The production site at `ai-access-observatory` is untouched and remains the live product.
