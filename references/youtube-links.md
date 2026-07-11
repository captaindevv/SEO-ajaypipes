# YouTube Video Inventory — Ajay Pipes

> Auto-loaded alongside `references/linking.md`. Supplements the engine's generic `skills/blog/references/video-embeds.md` (embed code, placement rules, VideoObject schema — still use that file for the *how*; this file governs the *which channel*).

## The rule

**Only embed or link videos from Ajay Pipes' own official YouTube channel.** Never embed a generic third-party "best pipe brand" or competitor-comparison video, even if it scores well on the generic engine's quality criteria (views, engagement, recency) — those videos routinely name competitors and rank pipe brands, which conflicts directly with `BRAND.md`'s "never write like the underdog" / no-competitor-names rule. A third-party video embedded in an Ajay post effectively hands the reader a comparison Ajay would never make in its own text.

## Official channel

- **Channel**: Ajay Pipes
- **URL**: https://www.youtube.com/channel/UCMKxcrWmX533hHt3ZdKHsQA
- **Verified**: 11 Jul 2026, directly from the footer of `ajaypipes.com/contact/` (the company's own site links to this channel — this is the primary-source confirmation, not a search-result guess).

## Known videos (verified via search 11 Jul 2026 — re-confirm titles/availability before embedding, channel content changes)

| Video Title | Topic Fit | URL |
|---|---|---|
| Ajay Pipes Introduction, and Complete Plumbing and Drainage Pipes & Fittings Product Range (#hindi) | General/intro, full product range, Hindi-language content | https://www.youtube.com/watch?v=EHT_Yxa4oeg |
| Complete Range of PVC, CPVC, UPVC, SWR & UDS Pipes and Fittings | General/intro, cross-product-line posts | https://www.youtube.com/watch?v=DfZV2xwxIFU |
| Ajay Pipes — largest manufacturer of CPVC Pipes and Fittings | CPVC/Flowline Plus posts | https://www.youtube.com/watch?v=TYT5I7WNEAU |
| Ajay Pipes Long Lasting Plumbing Solution (brass fittings, thermo-cycling test, anti-rodent, NSF certified, 50-year design life) | Quality/certification/durability posts, fittings posts | https://www.youtube.com/watch?v=GUk5u_09ZV0 |

These 4 were confirmed by title match against the verified channel; YouTube's page structure is JS-rendered so automated tools cannot always confirm the exact uploading channel handle from a static fetch. Before embedding, do a quick visual check that the video is still live and still carries Ajay Pipes branding.

## When no matching video exists

Most posts (especially the Deepline/borewell, Agriline/irrigation, Terraline/UDS, water-tank, and most fittings/valves categories in `references/internal-links.md`) have **no matching Ajay-owned video** in the list above. In that case:

1. **Do not substitute a third-party video** — that breaks the no-competitor-comparison rule above.
2. Re-run a search scoped to the channel (`site:youtube.com/channel/UCMKxcrWmX533hHt3ZdKHsQA [topic]` or `"Ajay Pipes" [topic] site:youtube.com`) to check whether a newer, more specific video has been published since this file was last updated.
3. If still nothing fits, skip the video embed entirely for that post. A missing video is not a quality failure — an off-brand competitor video embedded to satisfy a checklist is.

## Maintenance

Re-run the channel search periodically (the engine's `blog-google` YouTube search sub-feature, or a manual WebSearch scoped to the channel URL) and add newly published Ajay Pipes videos to the table above, tagged by topic fit.
