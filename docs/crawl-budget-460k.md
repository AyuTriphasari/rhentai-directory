# Crawl budget math for 460K URLs

Notes from running an archive this size ([RHentai](https://rhentai.tech),
420K+ galleries / 30K+ waifus / 14K+ videos). Companion to the
[rhentai-directory](https://github.com/AyuTriphasari/rhentai-directory).

## The naive numbers

At ~1 request/second, Googlebot needs ~5.3 days to fetch 462K URLs once.
Real crawlers fetch much less: realistic budget for a mid-authority domain is
thousands of URLs per day, not hundreds of thousands.

## What that implies

1. **Every wasted slot matters.** Redirects in sitemaps, duplicate parameter
   URLs, pages that 500 — each one displaces a real page.
2. **Chunked sitemaps must be honest.** 49 chunks, each verified 200. The
   index and generator share one source of truth (see
   [canonical policy](canonical-policy.md)).
3. **Internal links do the routing.** Sitemaps get pages *known*; hub pages
   (tag hubs, character pages) get them *crawled*. Both need to exist.
4. **Edge caching helps more than origin speed.** Sitemap chunks served with
   `s-maxage=3600` keep crawler traffic off the origin.

## The one-line health check

```
for i in $(seq 0 48); do curl -so /dev/null -w "%{http_code}
"   https://example.com/sitemap/$i.xml; done | sort | uniq -c
```

49 x `200` or investigate.

---

*Part of the rhentai-directory docs. Main page: [README](../README.md).*
