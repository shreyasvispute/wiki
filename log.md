# Wiki Log

> Append-only chronological record of wiki activity. Each entry starts with `## [date] action | description` for easy parsing.
>
> Quick reference: `grep "^## \[" log.md | tail -10`

## [2026-04-14] init | Wiki created
- Structure: AGENTS.md, index.md, log.md
- Directories: raw/, sources/, entities/, concepts/, analyses/
- Ready for first source ingest

## [2026-04-14] ingest | MLB articles from raw/assets/links.md
- Processed 4 unique URLs (links 1 & 3 were duplicates); 3 fetched successfully, 1 failed (mlb.com Rule 4 Draft — redirect)
- Summary: sources/mlb-leagues-divisions-explained.md
- Summary: sources/sunday-night-baseball-2026-schedule.md
- Summary: sources/al-nl-rule-differences.md
- Pages created: entities/major-league-baseball.md, concepts/designated-hitter.md
- Pages updated: (none — first ingest)

## [2026-04-14] ingest | Minor League Baseball Ecosystem PDF
- Summary: sources/minor-league-baseball-ecosystem.md
- Pages created: entities/minor-league-baseball.md, concepts/mlb-player-development-pathways.md, concepts/mlb-scouting-evaluation.md, concepts/mlb-roster-mechanics.md
- Pages updated: entities/major-league-baseball.md (added Minor League System section and cross-links)
