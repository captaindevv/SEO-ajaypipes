# On-Page SEO — Ajay-Specific Findings

> This supplements the engine's built-in checklist (`skills/blog/references/quality-scoring.md`, `skills/blog-seo-check/SKILL.md`) — it does not replace it. Everything below is verified against the live site (ajaypipes.com, checked 9 Jul 2026), not assumed. Read this before running `blog-seo-check`, `blog-schema`, or `blog-geo` on any Ajay page — the generic checklist doesn't know these platform-specific facts.

## Schema — what's actually there vs actually missing

The site runs WordPress + Yoast SEO. Yoast auto-generates a schema graph on every page. Confirmed present sitewide (checked raw HTML, not inferred): `Organization`, `WebSite`, `WebPage`, `BreadcrumbList`, `Article`, `Person` (author).

**Do not tell the user or generate content claiming these are missing — they're not.** The actual gaps:

- **`FAQPage` schema — confirmed absent everywhere**, including on posts with a visible, rendered FAQ block (checked the top-traffic post directly). This is the real schema gap for blog posts. `blog-schema` should generate `FAQPage` JSON-LD for any post with an FAQ section; it does not need to touch Article/Breadcrumb/Person, those are already handled by Yoast.
- **`Product` schema — confirmed absent** on product pages (checked `/ajay-flowline-plus-cpvc-pipes-and-fittings/` directly). Product pages are not blog posts, so this is outside `blog-schema`'s normal remit — flag it as a separate task if the user asks for product-page schema, don't silently skip it.
- **Organization schema `name` field is lowercase**: `"ajay industrial corporation ltd"`. Cosmetic but real — worth a one-line fix note if anyone's touching Yoast's site-identity settings.

## Sitemap & crawl — a real technical gap, not "assume it's fine"

`sitemap.xml` is a **static, third-party-generated file** (via xml-sitemaps.com), frozen at `lastmod: 2024-06-03` on every single URL.

- **Zero 2025/2026 blog posts are in it** — the entire back half of the 102-post Blog Database, including everything in `references/used-keywords.md` published after mid-2024, is absent from the submitted sitemap.
- **~94 of 290 URLs (32%) are junk**: 55 category archive pages, 15 paginated author-archive pages, 24 blog-pagination pages, and one URL with a live Google Ads `gclid` tracking parameter baked into it.
- **`robots.txt` is empty** (200 OK, 0 bytes) — not blocking anything, but doesn't declare the sitemap location either.
- **`llms.txt` does not exist** (404) — no AI-crawler-specific guidance, relevant to `blog-geo` output.

**This is a platform/technical fix, not something a blog-content skill can resolve from inside a post.** If `blog-audit` or `blog-geo` flags indexation or freshness problems on Ajay content, the root cause is very likely this stale sitemap, not the content itself. Say so explicitly rather than recommending more content fixes.

## Confirmed live issues (not hypothetical, checked directly)

- **Cannibalization is still live, unresolved**: both `/cpvc-full-form/` and `/cpvc-pipe-full-form/` return HTTP 200 right now. Any new content plan should not assume this was fixed just because the strategy docs recommended it.
- **Flagship product page H1 has zero keyword content**: `/ajay-flowline-plus-cpvc-pipes-and-fittings/` H1 is literally "Flowline Plus" — no "CPVC Pipe," no product category term at all.
- **Product pages have no real CTA**: only generic "Contact Us." No "Get a Quote," "Request a Quote," or "Find a Dealer" — see `BRAND.md` Editorial Rules for the CTA language every new/rewritten commercial page should use instead.
- **Homepage says "50+ Years"**: stale by 15 years (1961 → 2026 = 65+). Any content referencing company age must use 65+, per `references/stats.md`. Flag the on-site copy separately — it wasn't changed as part of this content work.

## Mandatory additions for every Ajay blog post (on top of the engine's standard checklist)

1. `FAQPage` JSON-LD if the post has an FAQ section (it should — see engine's standard FAQ requirement).
2. At least one internal link to a specific product page with descriptive anchor text — this is the single most consequential fix on this site (see `BRAND.md`, `references/voice.md`). This site does not use the engine's generic 3–10-link default at all: `references/linking.md` sets a higher, word-count-tiered target (10 links under 1,000 words, 13-15 under 1,500, 15-20 above), and it is satisfied only if at least one link points to a product page, not just other blog posts.
3. Check `references/used-keywords.md` clusters before finalizing the primary keyword — three semantic-duplicate clusters already exist (~25 posts). Don't add a 26th.
4. No competitor names, no defensive/underdog framing — see `BRAND.md` taboo list.
