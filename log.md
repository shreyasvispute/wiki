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

## [2026-04-25] ingest | MiLB Teams by Affiliate (links 6 & 7)
- Processed 2 URLs; 1 fetched successfully (mlb.com/milb/about/teams/by-affiliate), 1 failed (mlb.com/milb — redirect to tracking pixel)
- Summary: sources/mlb-milb-teams-by-affiliate.md
- Pages created: (none)
- Pages updated: entities/minor-league-baseball.md (added Affiliated Teams section with 120-team count and patterns)

## [2026-04-25] ingest | MiLB Rookie Leagues — ACL, FCL, DSL (links 8–10)
- Processed 3 URLs; all 3 fetched successfully
- Summary: sources/milb-rookie-leagues.md
- Pages created: (none)
- Pages updated: entities/minor-league-baseball.md (expanded Rookie league details with DSL Cup, rebranding history, multi-squad notes)

## [2026-04-25] ingest + merge + analysis | Link 11, source consolidation, numbers summary
- Ingested link 11 (mlb.com/milb/about/teams/by-league) — all 11 full-season MiLB league names and rosters
- Merged sources/milb-rookie-leagues.md into sources/mlb-milb-teams-by-affiliate.md → single consolidated "MLB Minor League Teams: Complete Reference" with affiliate tables, league directory, and full Rookie league detail
- Deleted sources/milb-rookie-leagues.md (duplicate content absorbed)
- Created analyses/mlb-milb-by-the-numbers.md — comprehensive numbers summary with tables for MLB org, MiLB structure, league sizes, roster rules, scouting scale, development timelines, and 2026 broadcasting
- Pages updated: entities/minor-league-baseball.md (fixed cross-references), index.md
