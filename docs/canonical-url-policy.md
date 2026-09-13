# Canonical URL policy for large archives

The canonical rules used by the [rhentai-directory](https://github.com/AyuTriphasari/rhentai-directory)
index, distilled from a live ~462K-URL archive ([RHentai](https://rhentai.tech)).

## The four rules

1. **One concept, one URL.** Gallery pages canonical to themselves; filtered
   tag combinations (`?tags=a+b`) are `noindex,follow` and canonical to the
   clean hub.
2. **Redirects never appear in sitemaps.** A submitted redirect wastes a crawl
   slot and reports as an error. We removed `/video/{slug}` from sitemaps
   entirely once it became a 307.
3. **Adult content gets explicit signals, not silence.** `robots.txt` declares
   which crawlers are welcome; content signals say `search=yes, ai-train=no`.
   Ambiguity is how sites get deindexed by accident.
4. **The sitemap index and chunk generator share one count query.** The
   incident: index promised 50 chunks, generator made 43, chunks 43-49
   returned HTTP 500 — a mass-crawl-error incident caused by two components
   counting with different filters.

## The integrity rule for inclusion

`num_pages >= 1` AND page data present. We retired a `favorites >= 100` gate
after it hid 62K perfectly indexable galleries. Niche is not thin content.

Result: 49 chunks, all HTTP 200, ~462K URLs admitted.

---

*Part of the rhentai-directory docs. Main page: [README](../README.md).*
