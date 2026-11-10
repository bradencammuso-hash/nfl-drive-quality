# Hidden Value: What Actually Makes an NFL Drive Successful?

A season-long analysis of the 2026 NFL season using drives as the unit of analysis. The project tracks drive quality, ranks teams and players each week, and projects game scores, which are then compared to the betting market.

Author: Braden Cammuso, Worcester Polytechnic Institute (Financial Technology)

## The question

Most team stats are per game or per play. This project looks at each drive instead and asks which things actually separate good drives from bad ones. It then uses those drive-level numbers to rank teams and project scores.

## Data

- Play-by-play, schedules, rosters, snap counts, injuries and contracts from [nflverse](https://github.com/nflverse), loaded in Python with `nflreadpy`
- 2026 regular season for the live analysis; 2015 to 2025 seasons for backtesting
- No data is hand-collected. Anyone can rebuild the dataset by running the pipeline notebook.

## Method

- **Drive as the unit:** each play is grouped into its drive, and drives are summarized (EPA, success rate, result, field position, and more)
- **Garbage time filter:** drives played when the game is already decided are removed so they don't inflate stats
- **40-drive gate:** a team needs at least 40 drives before its numbers are treated as reliable
- **Injury and starter adjustments:** projections account for key players who are out, including a new or backup QB
- **Backtesting:** projection models are tested on past seasons (2016 to 2025), with weights fitted on one set of seasons and checked on others, so results aren't judged on the same data they were built on

## Notebooks

| Notebook | What it does |
|---|---|
| `aa_WEEKLY_1_Phase2_Pipeline` | Pulls nflverse data and builds the clean drive-level dataset |
| `aa_WEEKLY_2_Points_Projection` | Projects each team's points for the coming week |
| `aa_WEEKLY_3_Points_Projection_advanced` | Advanced projection versions (QB history, injuries, weather, roster talent) with backtest results |
| `aa_WEEKLY_4_Weekly_Report` | Weekly summary of projections and results |
| `aa_WEEKLY_5_rankings` | Weekly team, offense, defense and player position rankings |
| `RESEARCH_Phase3_Exploration` | First look at what separates good and bad drives |
| `RESEARCH_Phase4_Analysis` | Main drive quality analysis |
| `RESEARCH_Defensive_Analysis` | Drive quality from the defensive side |

The `aa_WEEKLY` notebooks are rerun every week during the season, in order, before Sunday's games.

## Results so far

Backtest over ten seasons (2016 to 2025, 4,320 team scores):

| Model | Average miss (points per team) | Picks the winner |
|---|---|---|
| Advanced projection | 7.38 | 64.2% |
| Advanced projection + roster talent | 7.37 | 65.3% |
| Betting market | 7.26 | 67.6% |

The model gets close to the betting line but doesn't beat it yet. Adding roster talent (based on contract value and snap share) improved winner picks in 7 of 10 seasons but did not meaningfully improve the point projections, so it is being tracked as a separate trial version instead of replacing the main model.

## What I learned

- The betting market is hard to beat because it already prices in things like injuries and talent
- Small samples early in the season can mislead. A backup QB topped the QB rankings after two games, which led to adding the 40-drive gate and starter adjustments
- Any new idea has to pass a set rule on held-out seasons before it is adopted, so the model isn't tuned to look good after the fact

## Next steps

- Keep tracking 2026 projections live each week against the line
- Full write-up of the drive quality findings after the Super Bowl

## Tools

Python (pandas, nflreadpy), Jupyter, Excel. I use AI as a coding assistant to turn my designs into code faster. The question, method, filters and checks are mine, and I test and review everything it produces.
