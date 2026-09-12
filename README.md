# RHentai — waifu & doujin explorer

Public directory for **RHentai** ([rhentai.tech](https://rhentai.tech)) — a doujin reader, waifu
database and h-anime streaming platform. Adult content, 18+.

## Catalog

- **420K+ doujin galleries** with page data, tags and related items
- **30K+ waifu character profiles**
- **14K+ h-anime videos** in a separate, canonical-clean section
- **Hundreds of tag hubs** (full color, AI generated, uncensored, ...) with stable URLs and real descriptions

## Engineering notes

This repo documents the boring-but-critical parts of running a ~462K-URL adult archive:

- Sitemap delivered in 49 chunks, all verified 200 (single source of truth between index and generator)
- One canonical URL per concept; filtered tag combos are `noindex, follow` → canonical to clean hub
- Data-integrity filter (`num_pages >= 1` + page data presence) instead of popularity filters
- Hourly crawl → staging → merge pipeline (`ON CONFLICT ... IS DISTINCT FROM`)
- Explicit robots.txt crawler policy with declared content signals

## Links

- Site: <https://rhentai.tech>

*This is an unofficial/support repository maintained by a contributor.*
