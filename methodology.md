# The BestRobotMower Score: methodology

The `bestrobotmower_score` in this dataset is a transparent **0-5** rating (one decimal) for each **shipping**
robot mower. It is **not** a user poll or an editor's opinion. It is a documented weighted average of five
capability axes, each computed from the same cited specs shown in this dataset. Change a spec or a price and the
score recomputes. Announced models are not scored, because you cannot recommend buying a machine you cannot buy.

The canonical, always-current version of this rubric lives at
[https://bestrobotmower.co/methodology?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset](https://bestrobotmower.co/methodology?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset).

## The five axes

Each axis is scored 0-5, then combined as a weighted average. Weights renormalise over the axes actually present
for a model (a model missing a datum drops that axis rather than scoring zero), so a score is only ever computed
from real numbers.

### 1. Navigation & mapping: weight 25%
Structural, from the positioning class. Tiers span 2.5-5.0 so the axis discriminates between machines:

| Capability | Sub-score |
|---|---|
| LiDAR **and** AI-camera obstacle avoidance | 5.0 |
| LiDAR (no obstacle camera) | 4.5 |
| RTK GNSS **and** AI-camera obstacle avoidance | 4.0 |
| RTK GNSS only | 3.4 |
| Camera-vision only (boundaryless) | 3.0 |
| Basic / none of the above | 2.5 |

### 2. Obstacle avoidance: weight 20%
Read from the cited obstacle-camera capability, **not** inferred from the nav class (an RTK mower can have a
camera; a LiDAR mower can lack one):

| Capability | Sub-score |
|---|---|
| Real AI-camera obstacle avoidance | 5.0 |
| LiDAR sensing, no obstacle camera | 3.3 |
| No obstacle camera | 2.0 |

### 3. Coverage: weight 20%
Rated maximum lawn area, square-root compressed onto a 2.3-5.0 band against the largest-coverage model tracked,
so an estate machine cannot run away with the score on scale alone and a right-sized small mower is not crushed.

`score = clamp(2.3 + 2.7 × sqrt(coverage / max_coverage_in_set), 1, 5)`

### 4. Slope & terrain: weight 15%
Rated maximum grade, normalised linearly to the steepest model tracked, on a 2.3-5.0 band.

`score = clamp(2.3 + 2.7 × (slope / max_slope_in_set), 1, 5)`

### 5. Coverage per dollar: weight 20%
The absolute $/m² ratio (price ÷ coverage), normalised so the best value in the field = 5 and the worst = 1.5.
This is an absolute value axis: a small, right-sized mower scores low here on a high $/m² even when it is the
best choice for a small lawn (a size-relative judgment made separately on the site's picks).

`score = clamp(5.0 − 3.5 × (ppm2 − min_ppm2) / (max_ppm2 − min_ppm2), 1, 5)`

## Combining

Each axis sub-score is rounded to one decimal first, then the overall is the weighted average of the rounded
axes (weights renormalised over the axes present), rounded to one decimal. So the headline score is exactly
reproducible from the per-axis figures (`score_navigation`, `score_obstacle_avoidance`, `score_coverage`,
`score_slope`, `score_coverage_per_dollar`) in [`data/mowers.json`](data/mowers.json).

A model needs the two structural axes plus at least one measured axis to receive a published score.

## Sources

Every coverage, slope, and price figure carries its own source URL in the dataset
(`coverage_source_url`, `slope_source_url`, `price_source_url`) pointing to the manufacturer spec sheet or the
retailer that proves the price. Prices are dated snapshots (`price_snapshot_date`), not live figures.
