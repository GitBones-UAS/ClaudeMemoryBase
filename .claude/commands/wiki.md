Answer the user's question by searching the vault wiki first, then the web only if needed.

**Goal: read the minimum number of pages that fully answer the question. Do not scan the whole wiki.**

1. **Extract keywords** from the question — concrete nouns, entity names, technologies, domains, acronyms. Include obvious synonyms and variants (e.g., "IPT" → also try "inductive power transfer").
2. **Filter the index first.** Grep `wiki/_index.md` for the keywords to find candidate page titles. If nothing hits, broaden: drop one keyword at a time, then try the domain folder name.
3. **Filter the wiki by content.** Grep across `wiki/**/*.md` for the keywords (use `files_with_matches` mode) to catch pages the index entry didn't surface. Combine with the index hits to form the candidate set.
4. **Rank and cap.** Prioritize: exact title match → entity/concept page → domain overview → source summaries → analyses. Read at most ~5 pages on the first pass. Only expand if the initial pages clearly leave the question unanswered.
5. **Follow wikilinks selectively** — only when a linked page is directly required to answer the question, not for general context. Each follow should be justifiable.
6. **Synthesize** from what you read, citing pages with `[[wikilinks]]`. If coverage is thin, say so explicitly rather than padding.
7. **If the wiki doesn't answer fully**, search the web for the missing pieces. Clearly label wiki vs. web in the response.
8. **If the synthesis is substantive and not already captured**, file it as an analysis page per CLAUDE.md schema (type: `analysis`, correct domain, update `wiki/_index.md`, append to `wiki/_log.md`).
9. **Keep the response to Sammy concise** — lead with the answer, follow with sources.
