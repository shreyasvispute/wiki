# Wiki Schema

This file defines how the LLM operates on this wiki. It is the single source of truth for conventions, workflows, and structure.

## Directory Structure

```
wiki/
├── AGENTS.md          # This file — schema and workflows
├── index.md           # Content catalog (LLM-maintained)
├── log.md             # Chronological activity log (append-only)
├── raw/               # Immutable source documents (human-managed)
│   └── assets/        # Downloaded images referenced by sources
├── sources/           # LLM-generated source summaries
├── entities/          # Pages for people, organizations, places
├── concepts/          # Pages for ideas, frameworks, themes
└── analyses/          # Filed query results, comparisons, syntheses
```

## Page Conventions

### Frontmatter

Every wiki page (except index.md and log.md) must have YAML frontmatter:

```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag1, tag2]
sources: [source-filename-1, source-filename-2]
---
```

### Naming

- Use lowercase kebab-case for filenames: `machine-learning.md`, `john-doe.md`
- Source summaries mirror the raw filename: `raw/paper.pdf` → `sources/paper.md`

### Linking

- Use standard markdown links with relative paths: `[Page Title](../concepts/topic.md)`
- When referencing sources, link to the summary page, not the raw file
- Every page should link to at least one other page — no orphans

### Content Style

- Write in clear, concise prose
- Use headers (##, ###) to structure longer pages
- Use bullet points for lists of facts or claims
- When information comes from a specific source, cite it inline: `(source: filename.md)`
- When new information contradicts existing content, note the contradiction explicitly

---

## Workflows

### 1. Ingest

Triggered when the user adds a new file to `raw/` and asks the LLM to process it.

**Steps:**

1. Read the source document in `raw/`
2. Discuss key takeaways with the user (unless told to batch-process silently)
3. Create a summary page in `sources/` with:
   - Frontmatter (title, date, tags, source reference)
   - A structured summary of the source's key points
   - Notable claims, data, or arguments
   - Questions raised or gaps identified
4. Update existing wiki pages:
   - If entities mentioned in the source already have pages → update them with new info
   - If concepts mentioned already have pages → update them
   - If new entities or concepts are significant → create new pages in `entities/` or `concepts/`
5. Update `index.md` — add the new source summary and any new pages
6. Append an entry to `log.md`

**Log entry format:**
```
## [YYYY-MM-DD] ingest | Source Title
- Summary: sources/filename.md
- Pages created: entities/new-entity.md, concepts/new-concept.md
- Pages updated: entities/existing.md, concepts/existing.md
```

### 2. Query

Triggered when the user asks a question about the wiki's content.

**Steps:**

1. Read `index.md` to identify relevant pages
2. Read the relevant pages
3. Synthesize an answer with citations to specific wiki pages
4. If the answer is substantial and reusable, offer to file it as a new page in `analyses/`
5. If filed, update `index.md` and append to `log.md`

**Log entry format:**
```
## [YYYY-MM-DD] query | Brief description of question
- Answer filed: analyses/filename.md (or "answered in chat")
- Pages referenced: list of pages consulted
```

### 3. Lint

Triggered when the user asks for a health check, or periodically by the LLM's judgment.

**Steps:**

1. Read all pages and check for:
   - **Contradictions**: pages making conflicting claims
   - **Stale content**: claims superseded by newer sources
   - **Orphan pages**: pages with no inbound links
   - **Missing pages**: entities or concepts mentioned but lacking their own page
   - **Missing cross-references**: pages that should link to each other but don't
   - **Data gaps**: areas where a web search or new source could fill in missing info
2. Report findings to the user
3. Fix issues with user approval
4. Append to `log.md`

**Log entry format:**
```
## [YYYY-MM-DD] lint | Health check
- Issues found: N
- Issues fixed: N
- Details: brief summary
```

---

## Guidelines for the LLM

- **Never modify files in `raw/`.** That directory is owned by the human.
- **Always update `index.md` and `log.md`** after any ingest or filing operation.
- **Prefer updating existing pages** over creating new ones. Only create a new page when the topic is distinct enough to warrant it.
- **Flag contradictions explicitly** rather than silently overwriting. Use a blockquote:
  > ⚠️ **Contradiction**: Source A claims X, but Source B claims Y. (See: [A](../sources/a.md), [B](../sources/b.md))
- **Keep pages focused.** One entity per entity page, one concept per concept page. If a page is getting long, consider splitting it.
- **Cite sources inline.** Don't make claims without attribution.
- **Ask before making large structural changes** (e.g., reorganizing categories, merging pages).
