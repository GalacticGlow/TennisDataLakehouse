**TennisDataLakehouse**

This is a data lakehouse built on Databricks that contains processed and cleaned archive data about tennis from all across history to the present day, players from all around the world, as well as all the tournaments and championships they played in, and their world rankings and how they changed over time.

This dataset will be useful for anyone who is interested in tennis and its history, and who wishes to analyze things like the number of victories of different countries' players throughout history, how the global tennis rankings changed over time, what tournaments did the highest-ranked players play in, and so on, and the results of said findings can be visually shown using graphs in PowerBI or Tableau

This data is **open-source** and may be used by **anyone** for any purpose, however **please credit this repository as your source**

**Here is the data catalog for all 3 tables, with all the information you will need:**

**1. gold.dim_players**
- Purpose: stores data about tennis players throughout history and from all over the world, with ids to their articles on the official ATP website
- **Columns:**

| Column Name      | Data Type | Description                                                                                            |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------ |
| `player_id`      | bigint    | Unique internal identifier for each player. Used as the primary key to link player data across tables. |
| `first_name`     | string    | Player’s first (given) name.                                                                           |
| `last_name`      | string    | Player’s last (family) name.                                                                           |
| `hand`           | string    | Dominant playing hand of the player (e.g., left-handed, right-handed or ambidextruous).                               |
| `birth_date`     | date      | Player’s date of birth. Used to calculate age and eligibility.                                         |
| `country`        | string    | Country code or name representing the player’s nationality.                                            |
| `height`         | double    | Player’s height, typically measured in centimeters.                                                    |
| `wikidata_id`    | string    | External identifier linking the player to Wikidata (e.g., `Q54544`).                                   |

**2. gold.fact_rankings**
- Purpose: stores historical data about the world rankings of all tennis players and how said rankings changed over time. There is one record per player per date when the update of the points took place
- **Columns:**

| Column Name      | Data Type | Description                                                                                           |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------- |
| `ranking_date`   | date      | The date of the ranking snapshot. Represents when the ranking was recorded.                           |
| `player_rank`    | bigint    | The player’s global ranking position on the given date (lower values indicate better rankings).       |
| `player_id`      | bigint    | Unique identifier of the player. Foreign key referencing the player entity.                           |
| `current_points` | double    | Total ranking points accumulated by the player at the given date. Used to determine ranking position. |

**3. gold.fact_matches**
- Purpose: stores historical data about the solo tennis championships that have ever been held in history, along with all their matches and all the winners and losers of said matches. There is one record per championship/tournament per date per round played in said tournament
- **Columns:**

| Column Name              | Data Type | Description                                                      |
| ------------------------ | --------- | ---------------------------------------------------------------- |
| `record_id`              | int       | Unique identifier for each match record (surrogate primary key). |
| `tournament_name`        | string    | Name of the tournament where the match was played.               |
| `surface`                | string    | Type of court surface (e.g., clay, grass, hard).                 |
| `draw_size`              | int       | Number of players in the tournament draw.                        |
| `tournament_level`       | string    | Level/category of the tournament (e.g., Grand Slam, ATP 1000).   |
| `tournament_date`        | date      | Start date of the tournament.                                    |
| `match_number`           | int       | Identifier of the match within the tournament draw.              |
| `winner_id`              | bigint    | Unique identifier of the match winner (foreign key to player).   |
| `winner_seed`            | int       | Tournament seed assigned to the winning player.                  |
| `winner_entry`           | string    | Entry type of the winner (e.g., Q, WC, LL).                      |
| `winner_age`             | int       | Age of the winning player at the time of the match.              |
| `loser_id`               | bigint    | Unique identifier of the match loser (foreign key to player).    |
| `loser_seed`             | int       | Tournament seed assigned to the losing player.                   |
| `loser_entry`            | string    | Entry type of the loser (e.g., Q, WC, LL).                       |
| `loser_age`              | int       | Age of the losing player at the time of the match.               |
| `score`                  | string    | Match score (e.g., "6-4 7-6"). May include tiebreak details.     |
| `best_of`                | int       | Number of sets required to win the match (typically 3 or 5).     |
| `round`                  | string    | Tournament round (e.g., R32, QF, SF, F).                         |
| `match_duration_minutes` | bigint    | Duration of the match in minutes.                                |
