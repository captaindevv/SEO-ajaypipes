# Ajay Pipes — Blog Content Engine

This is `claude-blog` (30 sub-skills, 5 agents, 5-category 100-point scoring, GEO/AEO optimization — see `docs/ARCHITECTURE.md` for the full engine design) customized for **Ajay Industrial Corporation Ltd (Ajay Pipes)**, ajaypipes.com, via the engine's native `BRAND.md`/`VOICE.md` auto-load hook (`skills/blog-brand/SKILL.md`).

**Do not hand-edit the 30 files under `skills/*/SKILL.md` to "Ajay-ify" them.** They're generic, tested, security-hardened engine code — that's the point of the BRAND.md/VOICE.md pattern. All Ajay-specific context lives in the files below, and every drafting/reviewing/scoring sub-skill auto-loads them.

## Read before any blog command

1. `BRAND.md` — audience, positioning, editorial rules, taboo phrases, topic scope
2. `VOICE.md` — tone, sentence/paragraph ceilings, headline patterns
3. `references/voice.md` — full sentence rhythm and "tells it's AI-written" checklist
4. `references/humour.md` — the dry-to-warm personality dial (no puns, no mandatory jokes — different from this engine's other deployments)
5. `references/stats.md` — the only source for numbers. Never round, never invent, never use an SEO/competitive metric in reader-facing content
6. `references/stories.md` / `references/opinions.md` — real material only, one each per post max, never invented (populate these as real material is supplied — do not fabricate placeholder anecdotes)
7. `references/used-keywords.md` — check before picking any primary keyword; **3 known semantic-cannibalization clusters already exist covering ~25 of the 102 published posts** ("best/top pipe company," "best pipe for plumbing," "which pipe is best") — don't add to them
8. `references/linking.md` — internal/external link density rules by word count (defaults: 10 links under 1,000 words, 13-15 under 1,500, 15-20 above 1,500); pairs with `references/internal-links.md` (product pages + 102 blog posts, tagged by topic), `references/external-links.md` (11 verified press mentions + government/standards sources — never the syndication-network rows in Sheet1), and `references/youtube-links.md` (Ajay's own channel only, never a third-party video)
9. `on-page-seo-ajaypipes.md` — real, verified platform findings (schema gaps, stale sitemap, live cannibalization URLs) that the engine's generic checklist doesn't know about

## The business

Ajay Industrial Corporation Ltd, brand Ajay Pipes. Founded 1961 (65+ years). Sahibabad, Ghaziabad, UP. Oldest UPVC pipe ISI-license holder in India. 6 product lines: Flowline Plus (CPVC), Greenline (UPVC), Drainline (SWR), Terraline (UDS), Agriline (irrigation), Deepline (borewell). Full facts in `references/stats.md`.

**WordPress site (Yoast SEO plugin), not this repo's own stack.** Output format for anything destined for ajaypipes.com is HTML/Gutenberg-compatible markdown, not MDX/JSX. The engine's platform-detection table in `skills/blog/SKILL.md` already covers WordPress — default to that.

## The one rule above all others

**Never write like the underdog.** Ajay is not the biggest player in its market (Supreme, Astral, Finolex, Ashirvad outscale it) — none of that belongs in content. No competitor names, no defensive framing, no comparison-based confidence. Every claim of authority traces to a real, verifiable Ajay fact. See `BRAND.md` Editorial Rules and `references/voice.md`.

## Known state (don't assume these are fixed — verified 9 Jul 2026)

- Keyword cannibalization between `/cpvc-full-form/` and `/cpvc-pipe-full-form/` is still live
- Sitemap.xml is stale (frozen since 2024-06-03), missing all 2025/2026 content — a platform issue, not something content fixes alone will solve
- FAQPage and Product schema are the real gaps (Organization/WebSite/Article/Breadcrumb/Person already exist via Yoast — don't claim otherwise)
- 102 blog posts published Sept 2024–Jul 2026, 100% classified informational, ~25 of them are near-duplicate "best pipe company/brand" intent

Full detail: the SEO strategy docs at `../seo stragey/important folder/` (3-Month and Master 90-Day strategies) and the technical audit findings summarized in `on-page-seo-ajaypipes.md`.

## Everything else

Follow the engine as documented in `docs/ARCHITECTURE.md`, `docs/COMMANDS.md`, and `skills/blog/SKILL.md` (quality gates, scoring, the 6 Pillars, delivery contract). Nothing about the mechanics changes for Ajay — only the voice, facts, and keyword-selection guardrails layered on top via the files above.
