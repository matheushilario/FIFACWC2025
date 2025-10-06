# Data Dictionary — FIFA CWC 2025 Project

## Dimensions
**Dim_Team**
- `team_id` — unique team key
- `team_name` — club name
- `confederation` — AFC / CAF / CONCACAF / CONMEBOL / OFC / UEFA
- `country`, `city`, `founded_year`, `stadium_name`, `stadium_capacity`
- `market_value_eur` — total squad value (EUR)
- `qualification_method`, `notes` — context

**Dim_Players**
- `player_id`, `player_name`
- `position`, `nationality`, `birth_year` (if present)
- (Used for goal attribution and potential extensions like per-90 analysis.)

**Dim_Venue**
- `venue_id`, `stadium`, `city`, `capacity`

## Facts
**Fact_Matches**
- `match_id`, `match_number`
- `stage` — Group Stage / Knockout Stage
- `round` — Round 1–3 (groups) | Round of 16 | Quarterfinals | Semifinals | Final
- `group` — Group A–H (group phase)
- `date`, `time`, `venue_id`, `attendance`
- `home_team_id`, `away_team_id`

**Fact_MatchResults**
- `match_id`
- `home_score`, `away_score`
- `total_goals` — sum of team goals
- `goal_difference` — |home - away|
- `match_result` — Home Win / Away Win / Draw
- `player_of_match`
- `home_penalti`, `away_penalti` — penalty goals flags (0/1)

**Fact_Goals**
- `match_id`
- `team_id`, `player_id`
- `team_name`, `player_name`
- `minute`, `extra_time`
- `penalti` (0/1), `own_goal` (0/1)

**Fact_Stats**
- `match_id`
- `group` — “Match overview” category
- `statistic` — e.g., Ball possession, Big chances, Total shots, Saves, Corners
- `home`, `away` — numeric values per side

## Derived Metrics (used in analysis)
- **Group points** — 3/win, 1/draw, 0/loss
- **Goal Difference (GD)** — GF − GA
- **Market Value Rank (MV Rank)** — rank by `market_value_eur` (1 = highest)
- **Stage Reached** — Group / R16 / QF / SF / Runner-up / Champion
- **Performance Rank (proxy)** — tier-average: 1;2;3.5;6.5;12.5;24.5
- **Overperformance Δ** — `MV Rank − Performance Rank`
- **Offensive Efficiency** — Goals / Big Chances Created
- **Defensive Efficiency** — Goals Conceded / Big Chances Conceded

## Interpretation Notes
- **Overperformance Δ**: Positive values = exceeded financial expectations; negative = underachieved.
- **Efficiency**: High offensive efficiency suggests clinical finishing; low defensive ratio indicates strong resilience (goalkeeper + structure).