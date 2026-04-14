# Vault SJC — LLM Wiki Schema

This vault is a persistent, compounding knowledge base owned by Sammy (SJC). Claude Code maintains all wiki content. Sammy curates sources, directs analysis, and asks questions. Claude does the summarizing, cross-referencing, filing, and maintenance.

## Architecture

```
Vault SJC/
├── CLAUDE.md          # This file — schema and operating instructions
├── raw/               # Immutable sources — Claude reads, NEVER modifies
│   ├── articles/      # Web clips (all topics, via Obsidian Web Clipper)
│   ├── pdfs/          # PDF documents
│   ├── notes/         # Sammy's personal notes
│   ├── images/        # Downloaded images from articles
│   └── erasmus/       # Erasmus Systems business docs, spreadsheets
├── wiki/              # LLM-generated content — Claude owns entirely
│   ├── _index.md      # Master catalog of all wiki pages
│   ├── _log.md        # Chronological record of all operations
│   ├── _overview.md   # High-level synthesis across all domains
│   ├── erasmus/       # Erasmus Systems startup
│   ├── personal/      # Personal development, goals, self-improvement
│   ├── hobbies/       # Woodworking, cooking, reading
│   ├── oracle/        # Oracle career, LDP program
│   ├── markets/       # Financial markets, trading, macro
│   ├── coding-ai/     # Programming, AI/LLMs, tools, projects
│   ├── concepts/      # Cross-domain concept pages
│   └── entities/      # People, organizations, technologies
└── .obsidian/         # Obsidian configuration
```

## Rules

1. **Never modify files in `raw/`.** Sources are immutable. Claude reads them but never edits, moves, or deletes them.
2. **Claude owns `wiki/` entirely.** Create, update, and delete wiki pages freely. Sammy reads them in Obsidian.
3. **Every wiki page must have YAML frontmatter.** See templates below.
4. **Use `[[wikilinks]]` for all internal cross-references.** This is Obsidian-native and powers the graph view.
5. **Tags go in YAML frontmatter only**, not as inline hashtags. Format: `tags: [tag1, tag2]`
6. **Source summaries live in the primary domain folder**, with wikilinks connecting to other relevant domains.
7. **When a query produces a valuable synthesis, file it as a wiki page automatically.** Do not ask — just file it.
8. **Keep summaries to Sammy concise.** After batch operations, report: pages created/updated, key takeaways. No blow-by-blow.
9. **Entity pages should be comprehensive.** Include: description, leadership, financials, product lines, recent news, relevance to Sammy, sources.
10. **Reading notes track key takeaways and themes**, not world-building lore. Business/strategy books are the primary genre.

## Page Templates

### Source Summary
```yaml
---
title: "Source Title"
type: source-summary
domain: erasmus | personal | hobbies | oracle | markets | coding-ai
tags: [relevant, tags]
source_path: "raw/articles/filename.md"
source_url: "https://..."
author: "Author Name"
source_date: YYYY-MM-DD
date_created: YYYY-MM-DD
date_updated: YYYY-MM-DD
---

## Key Takeaways
- Bullet points

## Summary
Prose summary of the source.

## Relevance
How this connects to existing wiki knowledge.

## Related Pages
- [[wikilink to entity]]
- [[wikilink to concept]]
```

### Entity Page
```yaml
---
title: "Entity Name"
type: entity
entity_type: organization | person | technology | program
domain: erasmus | personal | hobbies | oracle | markets | coding-ai
tags: [relevant, tags]
date_created: YYYY-MM-DD
date_updated: YYYY-MM-DD
sources: ["raw/path/to/source.md"]
---

## Overview
What this entity is and why it matters.

## Details
Comprehensive profile — leadership, financials, product lines, capabilities, recent news as applicable.

## Relevance to Sammy
How this entity connects to Sammy's goals, projects, or interests.

## Related Pages
- [[wikilinks]]
```

### Concept Page
```yaml
---
title: "Concept Name"
type: concept
domain: erasmus | personal | hobbies | oracle | markets | coding-ai
tags: [relevant, tags]
date_created: YYYY-MM-DD
date_updated: YYYY-MM-DD
sources: ["raw/path/to/source.md"]
---

## Definition
Clear definition of the concept.

## Context
Where this concept appears and why it matters.

## Key Details
Technical details, data points, or analysis.

## Open Questions
Things not yet resolved or worth investigating further.

## Related Pages
- [[wikilinks]]
```

### Domain Overview
```yaml
---
title: "Domain Name — Overview"
type: domain-overview
domain: erasmus | personal | hobbies | oracle | markets | coding-ai
tags: []
date_created: YYYY-MM-DD
date_updated: YYYY-MM-DD
---

## Summary
High-level synthesis of everything in this domain.

## Key Pages
- [[wikilinks to most important pages]]

## Recent Activity
What's been added or changed recently.

## Gaps & Open Questions
What's missing, what should be investigated next.
```

### Comparison / Analysis
```yaml
---
title: "Analysis Title"
type: analysis
domain: erasmus | personal | hobbies | oracle | markets | coding-ai
tags: [relevant, tags]
date_created: YYYY-MM-DD
date_updated: YYYY-MM-DD
sources: ["raw/path/to/source.md"]
---

## Question
What question prompted this analysis.

## Findings
The synthesis / comparison / answer.

## Data
Tables, charts, or structured data if applicable.

## Related Pages
- [[wikilinks]]
```

### Book Page
```yaml
---
title: "Book Title"
type: book
author: "Author Name"
domain: hobbies
tags: [reading, genre-tags]
status: reading | completed | want-to-read
date_created: YYYY-MM-DD
date_updated: YYYY-MM-DD
---

## Key Takeaways
- Bullet points — the most important ideas from this book.

## Themes
Major themes and how they connect to Sammy's thinking.

## Notes
Detailed notes, organized by chapter or topic as appropriate.

## Related Pages
- [[wikilinks to concepts, entities, or other books]]
```

## Workflows

### Ingest

When Sammy adds a new source to `raw/` and asks Claude to process it:

#### Phase 1 — Read & Summarize (auto-commit)
1. **Read** the source file completely. For PDFs over 10 pages, read in chunks.
2. **Create a source summary page** in the primary domain folder under `wiki/`. Source summaries are 1:1 with raw sources and are always created automatically — no approval needed.

#### Phase 2 — Propose entities & concepts (STOP and wait)
3. **Compile a proposal** listing every new entity page and new concept page to create, plus any existing entity/concept pages that need updating. For each item include:
   - **Title** (as it would appear in `[[wikilinks]]`)
   - **Type** (entity or concept; for updates, note "update")
   - **One-line rationale**
4. **Present the proposal to Sammy and wait for approval.** Sammy may approve as-is, remove items, add items, rename items, or say "skip" to create no new entity/concept pages. **Do not proceed to Phase 3 until Sammy responds.**

#### Phase 3 — Commit approved pages & cross-reference
5. **Create only the approved** entity and concept pages. Apply approved updates to existing pages.
6. **Update the domain overview** page if one exists for the primary domain.
7. **Update existing analysis pages**: scan all existing `type: analysis` pages (competitive landscapes, market analyses, etc.) and update any whose topic is touched by the new source. A new source with competitive data, architectural parallels, or new evidence belongs in the relevant analysis page — not only in its own source summary.
8. **Cross-reference — bidirectional**: for every connection identified, update BOTH pages. If Page A links to Page B, open Page B and add Page A to its Related Pages. This applies to all page types: source-summary, entity, concept, domain-overview, analysis, and book. Never leave a one-directional link.
9. **Update `wiki/_index.md`** — add entries for all new pages.
10. **Append to `wiki/_log.md`** — one entry with date, operation type, source name, and pages touched.
11. **Report to Sammy**: short summary — pages created/updated, 3-5 key takeaways.

### Query

When Sammy asks a question, read the minimum set of pages that answers it — do not scan the whole wiki:

1. **Extract keywords** from the question (entities, technologies, domains, acronyms + obvious synonyms).
2. **Filter the index** — Grep `wiki/_index.md` for those keywords to get candidate titles. If nothing hits, broaden by dropping a keyword or trying the domain name.
3. **Filter wiki content** — Grep `wiki/**/*.md` (`files_with_matches` mode) for the keywords to catch pages the index entry missed. Union with step 2 hits.
4. **Rank and cap** — prioritize exact title match → entity/concept → domain overview → source summary → analysis. Read ~5 pages max on the first pass; expand only if coverage is clearly insufficient.
5. **Follow wikilinks selectively** — only when a linked page is directly required, not for general context.
6. **Synthesize** with `[[wikilink]]` citations. If wiki coverage is thin, say so and supplement with the web (label wiki vs. web).
7. **If the synthesis is substantive and not already captured**, file it as an analysis page in the appropriate domain folder and update the index.

### Lint

Weekly health check (runs Sunday 8:00 AM Eastern):

1. **Orphan pages** — wiki pages with no inbound links from other wiki pages.
2. **Missing pages** — entities or concepts mentioned in `[[wikilinks]]` that don't have their own page yet.
3. **Contradictions** — claims in one page that conflict with claims in another.
4. **Stale content** — pages that haven't been updated despite newer sources touching the same topic.
5. **Cross-reference gaps** — pages that should link to each other but don't.
6. **Domain overview drift** — domain overviews that don't reflect recent additions.
7. **Suggested sources** — gaps in knowledge that could be filled with a web search or new source.
8. Report findings and fix what can be fixed automatically. Flag contradictions and gaps for Sammy.

## Conventions

- **File naming**: lowercase, hyphens for spaces (e.g., `inductive-power-transfer.md`, `hii.md`)
- **Wikilinks**: use the page title, not file path (e.g., `[[Inductive Power Transfer]]`, `[[HII]]`)
- **Dates**: always YYYY-MM-DD format
- **Log entries**: `## [YYYY-MM-DD] verb | Title` (e.g., `## [2026-04-14] ingest | Erasmus Business Plan`)
- **Domain assignment**: a page belongs to the domain it most directly serves. Use wikilinks to connect across domains rather than duplicating content.
- **KalshiBot**: pages about KalshiBot span both `wiki/markets/` (strategy, market analysis) and `wiki/coding-ai/` (architecture, implementation). Use wikilinks between them.
