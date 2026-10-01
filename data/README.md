# Data

The full datasets are not committed to this repository. To reproduce the notebook, place the files below directly
in this `data/` folder. The notebook reads them from `../data/` relative to `notebooks/`.

`samples/` holds the first 100 rows of `TeamStatistics.csv` and `Games.csv` so the file formats can be inspected
without downloading the full data. The notebook does not read the samples.

## Input files

| File | Source | Size | Used for |
|------|--------|------|----------|
| `TeamStatistics.csv` | NBA Dataset: Box Scores and Stats (Kaggle) | 146,048 rows, 48 columns | Team box scores per game. Aggregated into regular-season team features (Section 3) and late-season form (Section 6). |
| `Games.csv` | NBA Dataset: Box Scores and Stats (Kaggle) | 73,023 rows, 22 columns | One row per game. Game type and playoff round labels build the target variable (Section 2) and identify regular-season games. |
| `PlayerStatistics.csv` | NBA Dataset: Box Scores and Stats (Kaggle) | 1,663,149 rows, 35 columns | Player box scores per game. Loaded in Section 1 but not used by the current model. |
| `combined_injuries_1997-2025.csv` | TBD | 31,915 rows, 9 columns (1997-2025) | Injury list transactions with `teamId` and `season`. Aggregated to regular-season injury counts per team-season (Section 8). |
| `injury_data.csv` | TBD | 16,873 rows, 5 columns (Oct 2016 to Jan 2025) | Additional injury list transactions from 2016-17 on. Combined with the file above for the regular-season versus playoff injury comparison. |

## Sources

- **Team, game, and player statistics:** Moore, E. A. *NBA Dataset: Box Scores and Stats (1947 - Today)*. Kaggle.
  https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores. The dataset is updated
  daily; the copy used here runs through March 22, 2026.
- **Injury data:** TBD. Both injury files share the format of Lauton, L. (2023). *NBA Player Injury Stats
  (1951-2023)*. Kaggle. https://www.kaggle.com/datasets/loganlauton/nba-injury-stats-1951-2023. They extend past
  2023, so the source of the later records is still being confirmed.

The v1 Excel study (`paper/v1_regression_study.pdf`) used data from Basketball Reference and does not rely on
these files.

## Columns the notebook relies on

- **`Games.csv`:** `gameId`, `gameDateTimeEst`, `hometeamId`, `awayteamId`, `winner`, `gameType`, `gameLabel`,
  `seriesGameNumber`
- **`TeamStatistics.csv`:** `gameId`, `gameDateTimeEst`, `teamId`, `win`, `teamScore`, `opponentScore`,
  `fieldGoalsAttempted`, `fieldGoalsMade`, `threePointersAttempted`, `threePointersMade`, `freeThrowsAttempted`,
  `freeThrowsMade`, `reboundsOffensive`, `reboundsDefensive`, `turnovers`, `assists`, `blocks`, `steals`
- **`combined_injuries_1997-2025.csv`:** `Date`, `Team`, `Acquired`, `Relinquished`, `Notes`, `season`, `teamId`
- **`injury_data.csv`:** `Date`, `Team`, `Acquired`, `Relinquished`, `Notes`

Team IDs follow the NBA's numbering (`1610612737` through `1610612766`).
