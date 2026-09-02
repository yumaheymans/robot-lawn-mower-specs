# Robot Lawn Mower Specs & Scores (Open Dataset)

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-blue.svg)](LICENSE)

An open, machine-readable dataset of **23 wire-free and RTK robot lawn mowers** across **9 brands**
(Dreame, EcoFlow, Ecovacs, Husqvarna, MOVA, Mammotion, Segway, Sunseeker, Worx), with cited specs, dated price snapshots, and a transparent **0-5 BestRobotMower Score**
for every shipping model.

Compiled and computed by **[BestRobotMower.co](https://bestrobotmower.co/?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset)**, an independent robot-mower comparison site.
Every spec links back to the manufacturer source that proves it, and every score is a documented function of
those specs (no user polls, no opinion). Released under **[CC BY 4.0](LICENSE)** so you can use it freely
with attribution.

> **Why this exists:** there was no open, structured spec table for robot mowers anywhere. Robotics hobbyists,
> Home Assistant tinkerers, journalists, and buyers kept re-scraping the same manufacturer PDFs. This is that
> table, kept honest and cited.

## Affiliate disclosure

BestRobotMower.co is an independent comparison site that earns affiliate commissions when readers buy through
some of its outbound links. **This dataset is the site's own compiled, cited data** (not scraped from third
parties, not fabricated), released under CC BY 4.0. The scores are computed from published specs and are not
influenced by affiliate relationships.

## What's inside

| File | Format | Rows |
|---|---|---|
| [`data/mowers.csv`](data/mowers.csv) | CSV (spreadsheet-friendly) | 23 |
| [`data/mowers.json`](data/mowers.json) | JSON (with dataset metadata + methodology block) | 23 |
| [`methodology.md`](methodology.md) | The full 0-5 scoring rubric | n/a |

- **21 shipping** models (buyable now, scored)
- **2 announced** models (revealed, not yet widely available, unscored)
- Prices last verified: **2026-08-24**

## Schema

| Column | Description |
|---|---|
| `brand` | Manufacturer (e.g. Segway, Mammotion). |
| `model` | Full model name. |
| `status` | `shipping` (buyable now) or `announced` (revealed, not yet widely available). |
| `release_year` | Year the model shipped, or was announced. |
| `navigation_type` | Compact navigation class: `RTK GNSS`, `RTK + Vision`, `LiDAR + Vision`. |
| `navigation_detail` | One-line description of the positioning/boundary system. |
| `all_wheel_drive` | Whether the model is all-wheel drive (matters on slopes/rough terrain). |
| `max_coverage_m2` | Manufacturer-rated maximum lawn area, in square metres. |
| `max_slope_pct` | Manufacturer-rated maximum slope, in percent grade. |
| `cutting_spec` | Cutting width, cut-height range, and noise where published. |
| `coverage_tiers` | Variants in the model family and the area each covers. |
| `lawn_size_class` | The lawn-size bucket(s) this model targets. |
| `price_snapshot_usd` | Cheapest tracked retail price (USD) at `price_snapshot_date`. A DATED SNAPSHOT, not a live price. |
| `price_snapshot_provider` | Retailer the snapshot price was tracked from. |
| `price_snapshot_date` | Date the price snapshot was verified. |
| `price_per_m2_usd` | price_snapshot_usd ÷ max_coverage_m2, a rough value indicator. |
| `bestrobotmower_score` | Transparent 0-5 BestRobotMower Score (shipping models only). See methodology below. |
| `score_navigation` | Sub-score, Navigation & mapping axis (weight 0.25). |
| `score_obstacle_avoidance` | Sub-score, Obstacle avoidance axis (weight 0.20). |
| `score_coverage` | Sub-score, Coverage axis (weight 0.20). |
| `score_slope` | Sub-score, Slope & terrain axis (weight 0.15). |
| `score_coverage_per_dollar` | Sub-score, Coverage per dollar axis (weight 0.20). |
| `model_page_url` | Link to the full model page on BestRobotMower.co, with cited sources. |
| `coverage_source_url` | Manufacturer source for the coverage figure. |
| `slope_source_url` | Manufacturer source for the slope figure. |
| `price_source_url` | Retailer source proving the price snapshot. |
| `summary` | One-line plain-language summary of the model. |

> **Price fields are dated snapshots**, not live prices. For the current price, open the `model_page_url` or
> `price_source_url`. Robot-mower prices move often; treat `price_snapshot_usd` as "cheapest tracked at
> `price_snapshot_date`."

## The BestRobotMower Score (0-5)

A documented weighted average of five capability axes, each read from the same cited specs in this dataset:

| Axis | Weight | Reads |
|---|---|---|
| Navigation & mapping | 25% | positioning class (RTK / LiDAR / vision) |
| Obstacle avoidance | 20% | whether it has an AI-camera obstacle system |
| Coverage | 20% | rated max lawn area |
| Slope & terrain | 15% | rated max slope |
| Coverage per dollar | 20% | price ÷ coverage |

Only **shipping** models are scored (you cannot recommend buying an announced machine). Full rubric with the
exact formulas: [`methodology.md`](methodology.md) and [https://bestrobotmower.co/methodology](https://bestrobotmower.co/methodology?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset).

## Shipping models (scored)

| Model | Brand | Navigation | Max coverage | Max slope | AWD | Price (snapshot) | Score |
|---|---|---|---|---|---|---|---|
| [Mammotion Luba 2 AWD 5000](https://bestrobotmower.co/mowers/mammotion-luba-2-awd-5000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK GNSS | 5,000 m² | 80% | Yes | $2,899 | **4.7** |
| [MOVA LiDAX Ultra 3000 AWD](https://bestrobotmower.co/mowers/mova-lidax-ultra-3000-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | MOVA | LiDAR + Vision | 3,035 m² | 80% | Yes | $2,399 | **4.7** |
| [Dreame Roboticmower A3 AWD Pro](https://bestrobotmower.co/mowers/dreame-roboticmower-a3-awd-pro?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Dreame | LiDAR + Vision | 2,500 m² | 80% | Yes | $2,249.99 | **4.6** |
| [Ecovacs Goat A2000 LiDAR PRO](https://bestrobotmower.co/mowers/ecovacs-goat-a2000-lidar-pro?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | LiDAR + Vision | 2,023 m² | 50% | No | $1,399 | **4.5** |
| [Ecovacs Goat G1](https://bestrobotmower.co/mowers/ecovacs-goat-g1?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | LiDAR + Vision | 1,600 m² | 45% | No | $1,599 | **4.3** |
| [Segway Navimow X330](https://bestrobotmower.co/mowers/segway-navimow-x330?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK + Vision | 3,000 m² | 50% | No | $2,299 | **4.3** |
| [MOVA LiDAX Ultra 1000](https://bestrobotmower.co/mowers/mova-lidax-ultra-1000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | MOVA | LiDAR + Vision | 1,000 m² | 45% | No | $999 | **4.2** |
| [Dreame A3 AWD](https://bestrobotmower.co/mowers/dreame-a3-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Dreame | LiDAR + Vision | 1,000 m² | 80% | Yes | $1,599.99 | **4** |
| [EcoFlow Blade](https://bestrobotmower.co/mowers/ecoflow-blade?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | EcoFlow | RTK GNSS | 2,800 m² | 27% | No | $2,899 | **4** |
| [Sunseeker X3 Plus](https://bestrobotmower.co/mowers/sunseeker-x3-plus?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Sunseeker | RTK + Vision | 1,200 m² | 30% | No | $999 | **4** |
| [Worx Landroid Vision WR220](https://bestrobotmower.co/mowers/worx-landroid-vision-wr220?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | Vision | 2,023 m² | 30% | No | $999.99 | **4** |
| [Mammotion Yuka 1500](https://bestrobotmower.co/mowers/mammotion-yuka-1500?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK + Vision | 1,500 m² | 45% | No | $1,799 | **3.9** |
| [Dreame Roboticmower A1](https://bestrobotmower.co/mowers/dreame-roboticmower-a1?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Dreame | LiDAR + Vision | 2,000 m² | 45% | No | $2,099 | **3.8** |
| [Ecovacs Goat O1200](https://bestrobotmower.co/mowers/ecovacs-goat-o1200?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | RTK + Vision | 1,200 m² | 45% | No | $1,499 | **3.8** |
| [Mammotion Luba 2 AWD 1000](https://bestrobotmower.co/mowers/mammotion-luba-2-awd-1000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK GNSS | 1,000 m² | 80% | Yes | $1,599 | **3.8** |
| [Mammotion Yuka Mini](https://bestrobotmower.co/mowers/mammotion-yuka-mini?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK + Vision | 809 m² | 50% | No | $999 | **3.8** |
| [Segway Navimow i110N](https://bestrobotmower.co/mowers/segway-navimow-i110n?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK GNSS | 1,012 m² | 30% | No | $1,099 | **3.8** |
| [Worx Landroid Vision Cloud](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 1,012 m² | 35% | No | $1,199 | **3.8** |
| [Husqvarna Automower 435 iQ AWD](https://bestrobotmower.co/mowers/husqvarna-automower-435-iq-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Husqvarna | RTK GNSS | 5,261 m² | 70% | Yes | $4,999 | **3.7** |
| [Segway Navimow i105E](https://bestrobotmower.co/mowers/segway-navimow-i105e?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK GNSS | 506 m² | 30% | No | $799 | **3.4** |
| [Husqvarna Automower 410 iQ](https://bestrobotmower.co/mowers/husqvarna-automower-410-iq?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Husqvarna | RTK GNSS | 2,023 m² | 45% | No | $2,999 | **3** |

## Announced models (not yet scored)

| Model | Brand | Navigation | Max coverage | Max slope | AWD | Est. price |
|---|---|---|---|---|---|---|
| [Ecovacs Goat A3000 LiDAR](https://bestrobotmower.co/mowers/ecovacs-goat-a3000-lidar?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | RTK + Vision | 3,035 m² | 50% | No | $1,910 |
| [Segway Navimow X390](https://bestrobotmower.co/mowers/segway-navimow-x390?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK + Vision | 10,118 m² | 50% | No | $4,499 |

## Using & citing

Free to use, adapt, and redistribute under CC BY 4.0 with attribution. Suggested citation:

> Robot Lawn Mower Specs & Scores dataset, BestRobotMower.co, https://bestrobotmower.co, 2026-09-02. Licensed CC BY 4.0.

If you build something with this (a comparison tool, a Home Assistant integration, a chart), open an issue or PR
and it can be linked here.

## Updating

Specs and prices drift. This snapshot was compiled **2026-09-02** (prices verified **2026-08-24**).
The live, continuously-updated version of every figure here is on the model pages at
[BestRobotMower.co](https://bestrobotmower.co/mowers?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset).

---

Data and scores © BestRobotMower.co, released under [CC BY 4.0](LICENSE). Built and maintained alongside
[bestrobotmower.co](https://bestrobotmower.co/?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset): independent robot-mower comparisons covering specs, prices, and navigation.
