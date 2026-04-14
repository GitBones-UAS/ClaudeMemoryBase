Run a lint health check on the Vault SJC wiki. Follow the CLAUDE.md schema's Lint workflow.

1. Read `wiki/_index.md` to get the full page list
2. Read every wiki page systematically and check for:
   - **Duplicate nodes** — two or more pages that represent the same entity or concept, or wikilinks that reference the same thing under slightly different names (e.g. `[[DMO]]` and `[[Distributed Maritime Operations]]`, or `[[Northrop]]` and `[[Northrop Grumman]]`). Signals: (a) two files whose titles are near-synonyms; (b) wikilinks in the corpus that point to a non-existent page where an existing page clearly covers the same subject; (c) Obsidian graph nodes that appear twice for what should be one concept.
   - **Orphan pages** — wiki pages with no inbound `[[wikilinks]]` from other wiki pages
   - **Missing pages** — entities or concepts referenced in `[[wikilinks]]` that don't have their own page yet
   - **Contradictions** — claims in one page that conflict with claims in another
   - **Stale content** — pages that haven't been updated despite newer sources touching the same topic
   - **Cross-reference gaps** — pages that should link to each other but don't
   - **Domain overview drift** — domain overviews that don't reflect recent additions
   - **Suggested sources** — gaps in knowledge that could be filled with a web search or new source

3. Fix what can be fixed automatically:
   - **Merge duplicate nodes**: For each duplicate pair, (1) choose the canonical page — prefer the more complete file, or the one with more inbound links, or the one whose filename matches the CLAUDE.md naming convention; (2) merge any unique content from the redundant page into the canonical page; (3) grep every wiki file for wikilinks pointing to the redundant title and rewrite them to point to the canonical title; (4) delete the redundant file; (5) remove the redundant entry from `wiki/_index.md`. For *link-only* duplicates (no redundant file exists, just inconsistent wikilink text), rewrite all variant links to the canonical form so Obsidian resolves them to one node.
   - Add missing cross-references between related pages
   - Update domain overviews to reflect recent additions
   - Create stub pages for missing wikilink targets
   - Update `wiki/_index.md` with any new pages

4. Report findings to the user:
   - List contradictions found (with page references)
   - List knowledge gaps worth investigating
   - List suggested new sources to look for
   - Summary of automatic fixes applied

5. Append a lint entry to `wiki/_log.md`:
   ```
   ## [YYYY-MM-DD] lint | Weekly Health Check
   - Pages scanned: N
   - Issues found: N
   - Auto-fixed: N
   - Needs review: [list]
   ```
