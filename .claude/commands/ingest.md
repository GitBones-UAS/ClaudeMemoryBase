Ingest all new, unprocessed sources in the vault.


1. Read `wiki/_log.md` to determine which source files have already been ingested.
2. Scan all files in `raw/` (including subdirectories) — exclude `.gitkeep` files.
3. Identify any source files that are NOT referenced in the log as already ingested.
4. For each new source, follow the Ingest workflow defined in `CLAUDE.md`:
   a. Read the source file completely (for PDFs over 10 pages, read in chunks)
   b. Create a source summary page in the primary domain folder under `wiki/`
   c. Create or update entity pages in `wiki/entities/`
   d. Create or update concept pages in `wiki/concepts/`
   e. Update the domain overview if one exists
   f. Update existing analysis pages (`type: analysis`) whose topic is touched by the new source — competitive data, architectural parallels, and new evidence belong in the relevant analysis page, not only in the source summary
   g. Add `[[wikilinks]]` cross-references — BIDIRECTIONAL. For every link added to a new page pointing at an existing page, open that existing page and add the reciprocal link back. No one-directional links.
   h. Update `wiki/_index.md`
   i. Append to `wiki/_log.md`
5. After processing all new sources, give a short summary: number of sources processed, pages created/updated, key takeaways.

If no new sources are found, report that the wiki is up to date.
