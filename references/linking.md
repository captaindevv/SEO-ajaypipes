# Linking Rules — Ajay Pipes

> Auto-loaded by every drafting/reviewing sub-skill that loads `BRAND.md` (`blog-write`, `blog-rewrite`, `blog-brief`, `blog-outline`, `blog-calendar`, `blog-strategy`, `blog-analyze`, `blog-audit`, `blog-geo`, `blog-cluster`, `blog-multilingual` — per `skills/blog/SKILL.md`'s BRAND.md/VOICE.md scope). Last updated: 11 Jul 2026.
>
> **This file overrides the generic engine defaults** in `skills/blog/references/internal-linking.md` (which caps at 3-10 links per post) for Ajay content specifically. The generic file's *mechanics* — anchor text quality rules, placement priority, bidirectional linking, orphan-page/cannibalization detection — still apply. Only the **density targets and hard caps** are superseded by the tiers below. Do not edit `skills/blog/references/internal-linking.md` itself; it's shared engine code used by other brand deployments. See `CLAUDE.md` for why Ajay-specific rules live here instead of in the shared skill files.
>
> Link *targets* (which URLs are eligible) come from `references/internal-links.md` (internal) and `references/external-links.md` (external, press mentions + government sources) and `references/youtube-links.md` (video). This file governs *how many* and *what mix*.

## Link density by word count

| Post Length | Total Links (anchor text) | External Links (subset) | Internal Links (remainder) |
|---|---|---|---|
| Under 1,000 words | **at least 10** | 2-3 | ~7-8 |
| 1,000-1,500 words | **13-15** | 3-4 | ~9-12 |
| Over 1,500 words (up to 2,500+) | **15-20** | 3-4 | ~11-17 |

These are the **default** targets for any post written or rewritten for ajaypipes.com. They apply automatically — the user does not need to request them every time.

**Override clause**: if the user's prompt explicitly asks to cap, reduce, or otherwise change the link count for a specific post ("just do 5 links," "no external links this time"), that instruction wins for that post. Absent an explicit instruction, use the table above.

## External link split (within the External Links subset above)

Every post's external links split across exactly two approved sources — never any other domain:

1. **1-2 links to a relevant press mention** from `references/external-links.md` section A (the 11 verified Tier-1 rows only — never the syndication-network rows, see that file for why).
2. **1-2 links to a government or internationally-recognized standards body** from `references/external-links.md` section B (BIS, CPHEEO, MoHUA, Jal Jeevan Mission, NSF).

Match both to the post's actual content — a press mention about "hidden cost of poor plumbing in construction" belongs in a contractor/builder-audience post, not a homeowner water-tank guide. A government source belongs where the post makes a claim that source actually substantiates (a CPVC hot-water post cites the BIS CPVC product manual or NSF; a borewell post cites Jal Jeevan Mission or CPHEEO). Don't drop a source in just to hit the quota — see the relevance rule below.

## Internal link composition (within the Internal Links remainder above)

- **At least 1 link to a product/money page** from `references/internal-links.md` (Products, Products/Landing Page, or Why Ajay/Audience section) — this is a hard floor per `BRAND.md` and `on-page-seo-ajaypipes.md`, not new to this file.
- The rest come from `references/internal-links.md`'s blog-post categories, prioritized by topical match to the post being written (see that file's "How to use this file" section).
- If a post's own category is thin (Agriline has only 2 blog posts; Drainline/SWR has only 1), draw the remainder from: the closest adjacent category, the relevant product page's sibling pages (e.g. all Drainline SWR fitting pages for a drainage post), the audience pages (home-owners/contractors/builders), and the About/trust pages — all before resorting to a link that isn't genuinely relevant.
- Check the Cannibalization Cluster flag in `references/internal-links.md` before linking heavily into the "best/top pipe company/brand" cluster — 1-2 supporting links are fine; don't make it the backbone of a new post's link strategy (see `references/used-keywords.md`).

## Relevance rule (overrides raw count when they conflict)

**Relevance decides every link; the count is the target, not a license to force irrelevant links.** The AI selects anchor text and destination based on genuine topical match to the surrounding sentence — never by mechanically working down a list to hit a number. If a post's topic genuinely doesn't support 10-20 relevant links (rare, given the breadth of `references/internal-links.md`), use fewer and don't manufacture a weak link just to satisfy the table. This is the same principle the shared engine states in `skills/blog/references/internal-linking.md`'s anchor-text rules; the Ajay-specific change is a higher target ceiling, not a license to abandon relevance.

## Anchor text — no link stuffing

The generic engine's anchor-text distribution and anti-pattern rules (`skills/blog/references/internal-linking.md` → Anchor Text Distribution, Anchor Text Anti-Patterns) apply in full at this higher volume:

- Descriptive, natural, varied anchor text — 2-6 words, never a full sentence, never "click here" / "read more" / "learn more" / a naked URL.
- **Never reuse the same anchor text for the same destination twice in one post**, and vary it across posts that link to the same page (see `BRAND.md`: "Ajay's Flowline Plus CPVC range," not "click here," and never the same phrase every time).
- **No paragraph gets more than 2 links.** At 15-20 links in a 2,500-word post, that's roughly one link per 125-165 words on average — spread them across the whole body, not front-loaded into the intro or back-loaded into a links list.
- If natural in-sentence placement runs out before the target count on a longer post, a short "Related reading" or "Explore more" list near the end (2-4 links max) is an acceptable release valve — but it should never be the primary mechanism, and it doesn't excuse using generic anchors even there.
- FAQ sections and citation capsules are legitimate, natural placements for a portion of the internal links — a "Related to [topic]? See our guide to [X]" inside an FAQ answer counts toward the target.

## Video links

Governed separately by `references/youtube-links.md` — only the official Ajay Pipes YouTube channel, never a third-party video. Video embeds are not counted against the anchor-text link totals in the table above (they're a distinct media element, per `skills/blog/references/video-embeds.md`'s 2-3-videos-per-post guidance).

## Quick reference for drafting

1. Determine target word count → look up the tier → note total link target, external split, internal split.
2. Pull the product page + topical blog posts from `references/internal-links.md`.
3. Pull 1-2 press mentions + 1-2 government sources from `references/external-links.md`, matched to actual claims in the draft.
4. Check `references/youtube-links.md` for a channel-matching video; skip if none fits (don't substitute a third-party video).
5. Write links in naturally, varying anchor text, respecting the 2-links-per-paragraph ceiling.
6. Before delivery, count: does the total hit the tier target? Does the external split match (1-2 press + 1-2 government)? Is there at least one product-page link? Any cannibalization-cluster links kept to a supporting role?
