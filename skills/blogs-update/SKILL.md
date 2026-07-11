---
name: blogs-update
description: >
  Ajay Pipes-specific catalog maintenance skill (not part of the generic
  30-skill engine — lives alongside it, reads/writes only the Ajay-specific
  data files). Logs new blog posts, press/article mentions, site pages, or
  YouTube videos into the link-inventory system that every drafting skill
  depends on: `references/internal-links.md`, `references/external-links.md`,
  `references/youtube-links.md`, `references/used-keywords.md`, and the
  three source CSVs (`Article and blogs - Sheet1/2/3.csv`). Not to be
  confused with `/blog update <file>`, which refreshes an existing post's
  stats via blog-rewrite — this skill adds NEW rows to the catalog, it
  never drafts or edits blog content. Use when the user says "blogs-update",
  "blog-update", "add this blog", "log this post", "we published X",
  "add a press mention", "new article about us", "add youtube video",
  "new page went live", "update the link database", "sync the catalog",
  "add to internal links", "add to external links".
user-invokable: true
argument-hint: "[add-blog|add-article|add-page|add-video|sync] <details>"
license: MIT
---

# Blogs Update: Catalog Maintenance for the Ajay Link Inventory

This skill keeps the Ajay-specific link-inventory files current as the business
publishes new content, gets a new press mention, ships a new site page, or
posts a new YouTube video. It is the only skill that writes to
`references/internal-links.md`, `references/external-links.md`,
`references/youtube-links.md`, and the three source CSVs — every drafting
skill (`blog-write`, `blog-brief`, `blog-rewrite`, `blog-outline`, etc.) reads
those files but never modifies them.

This skill is **Ajay-specific project tooling, not shared engine code** — it
lives beside the 30 generic `skills/*/SKILL.md` files described in
`CLAUDE.md` but is not one of them, so the "don't hand-edit the engine" rule
in `CLAUDE.md` doesn't apply to it. It exists specifically because that rule
means Ajay-only maintenance logic can't live inside the generic skills.

## Step 1: Identify the entry type

Read the user's prompt and determine which of the four types they're adding.
If it's ambiguous (e.g. they just paste a URL with no context), ask.

| Entry type | Destination files | Signal in prompt |
|---|---|---|
| **Blog post** | `internal-links.md`, `used-keywords.md`, Sheet2 CSV | A new ajaypipes.com blog URL, a title + primary keyword, "we published" |
| **Press/article mention** | `external-links.md`, Sheet1 CSV | A third-party publication name, "featured in," "coverage in," a non-ajaypipes.com news URL |
| **Site page** | `internal-links.md` (money-pages section), Sheet3 CSV | A new ajaypipes.com non-blog page (product, policy, audience page), "new page live" |
| **YouTube video** | `youtube-links.md` | A youtube.com URL, "new video," "uploaded" |

## Step 2: Collect required fields — never fabricate

If any required field is missing from the prompt, **ask for it**. Never invent
a URL, date, or keyword to fill a gap — this mirrors the root-level rule
against generating/guessing URLs, and a wrong URL in these files silently
breaks every future drafting skill that trusts them.

### Blog post
- Title (required)
- URL (required — must be on `ajaypipes.com`)
- Primary Keyword (required)
- Publish Date (required, `DD/MM/YYYY` to match the existing sheet format)
- Category (auto-derive per Step 3; user can override)

### Press/article mention
- Publication/outlet name (required)
- Language (required)
- Publish URL (required to be usable as a citation — if not yet live, log it with an empty URL and note "On Process," same as the existing sheet convention for untranslated/unpublished rows)
- English article doc link / translate doc link / image (optional, carry over if given)

### Site page
- Main Category (required — one of: Home Page, Products, Products / Landing Page, Why Ajay, About, About Ajay, Contact Us, Gallery, Legal, or a new category if genuinely new)
- Sub-Category / Sub-Category 2 (optional)
- URL (required — must be on `ajaypipes.com`)
- Title text (required)
- Meta description (optional)

### YouTube video
- Title (required)
- URL (required — must be `youtube.com/watch?v=...` or `youtube.com/embed/...`)
- Topic fit (required — which product line/content category this video supports)
- **Verify the channel**: confirm the video is on the confirmed Ajay Pipes channel (`https://www.youtube.com/channel/UCMKxcrWmX533hHt3ZdKHsQA`, per `references/youtube-links.md`). If the user gives a video from a different channel, stop and flag it — per `BRAND.md`, only Ajay's own channel is ever embedded, never a third-party video even if the user asks for one, since third-party pipe videos routinely name and rank competitors.

## Step 3: Categorize (blog posts only)

Apply the same keyword-substring categorization used to build the original
`internal-links.md`, in this priority order (first match wins):

1. `borewell`, `casing pipe`, `column pipe`, `deepline` → **Deepline — Borewell**
2. `agriculture`, `agriline`, `irrigation`, `farming` → **Agriline — Irrigation & Agriculture**
3. `water tank` → **Water Storage Tanks**
4. `swr`, `drainage`, `underground water supply`, `underground drainage`, `drain` → **Drainline/Terraline — SWR & Drainage**
5. `fitting`, `valve`, `elbow`, `socket`, `union`, `nrv`, `end cap`, `solvent`, `coupling`, `connection pipe` → **Pipe Fittings & Valves**
6. `cpvc` → **CPVC — Hot/Cold Water Plumbing**
7. `full form`, `what is`, `meaning` → **Definitional / "What Is" Guides**
8. `price`, `cost` → **Price & Cost Guides**
9. `upvc`, `pvc` → **UPVC/PVC — General Plumbing**
10. `company`, `manufacturer`, `brand`, `industry`, `supplier`, `dealer` → **Company / Brand / Industry Overview**
11. else → **General Plumbing**

Match against the title + primary keyword, lowercased.

### Cannibalization check (mandatory, warn don't block)

Check the new title against these four patterns (the same ones used to flag
the existing 25 posts):

- `best` + (`pipe`/`pvc`/`cpvc`) + (`company`/`brand`)
- `top` + (`pipe`/`pvc`/`cpvc`) + (`company`/`brand`)
- `which` + `pipe` + `best`
- `best` + `pipes?` + (`plumbing`/`home`/`house`)

If it matches, this is a candidate 4th entry into an already-saturated cluster
(see `references/used-keywords.md`). **Don't refuse to log it** (it may
already be published and needs to be in the catalog regardless), but
surface the warning clearly: name the cluster, note the new total, and
remind the user new content shouldn't add a 15th/26th entry — this is a
catalog-accuracy tool, not a publishing gate.

## Step 4: Write to the source CSV first

Append using the **exact existing column order** — do not reorder or add
columns:

- **Sheet1** (`Article and blogs - Sheet1.csv`): `newspaper name,Language,Image,English Article ,On Process ,Translate Article ,Publish URL,Update`
- **Sheet2** (`Article and blogs - Sheet2.csv`): `Company,Blog Title,Blog URL,Publication Date,Month,Year,Primary Keyword` — `Company` is always `Ajay Pipes`
- **Sheet3** (`Article and blogs - Sheet3.csv`): starts with **two blank columns**, then `Main Category,Sub - Category, Sub - Category 2,url,titleText,titleLength,metaDescription,metaDescriptionLength` — reproduce the two leading commas

Read the target CSV first, then use Edit to append the new row(s) at the end
(or Write only if doing a full regenerate — see Step 6).

## Step 5: Update the derived markdown file(s)

- **Blog post** → insert a row into the matching category table in
  `references/internal-links.md` (alphabetized by title within the category;
  update the post count in that section's heading), **and** append to the
  chronological table in `references/used-keywords.md` per that file's own
  "Log the new post here before publishing" rule.
- **Press mention** → before adding to `external-links.md` section A, check
  the outlet name isn't a syndication-network pattern (generic geography+news
  combinations like "Rajasthan Headlines," "Nagaland News 24x7" — see that
  file's exclusion note). If it looks like a syndication clone, warn the user
  and default to **not** adding it as a citable Tier-1 source; still fine to
  log in the CSV for record-keeping. If it's a genuine named masthead, add it
  with a topic-fit note (what the article is actually about) so future
  drafting can match it by relevance.
- **Site page** → add a row to the correct Main Category table in
  `references/internal-links.md`'s money-pages section.
- **YouTube video** → add a row to the table in `references/youtube-links.md`
  with its topic-fit tag.

## Step 6: Check for stale counts

Several files cite the total post count as a round number. If the new entry
changes it, update these too, in the same response:

- `CLAUDE.md` → "100 blog posts published Sept 2024–Jun 2026"
- `references/used-keywords.md` → "across ajaypipes.com's 100 published blog posts"
- `on-page-seo-ajaypipes.md` → "100 blog posts published... ~25 of them are near-duplicate"

Only touch the specific numbers affected — don't rewrite surrounding prose.

## Step 7: Report back

Summarize exactly what changed: which files were touched, which row(s) were
added, the assigned category, and any cannibalization or syndication-network
warning raised. Don't silently make judgment calls the user should see (e.g.
excluding a press mention as likely syndication) — always surface them.

## Bulk resync (fallback, not the default path)

For a full CSV re-import (e.g. the user hands over updated sheets with many
new rows at once) rather than logging one or two items conversationally,
prefer regenerating `internal-links.md` from the CSVs directly rather than
appending row-by-row — write a short Python pass (read all three CSVs, apply
the Step 3 categorization, emit the markdown tables) instead of hand-editing
the file 20+ times. Always diff against the current file before overwriting
so any manual annotations made in past `blogs-update` sessions aren't lost
silently.

## Guardrails

- Never fabricate a URL, publish date, or keyword — ask instead.
- Never add a YouTube video from a channel other than the confirmed Ajay Pipes channel.
- Never add a press-mention row to the citable Tier-1 table without checking it isn't a syndication-network clone.
- This skill only maintains data files. It never drafts, rewrites, or scores blog content — route those requests to `blog-write`, `blog-rewrite`, or `blog-analyze` instead.
