# Robot Lawn Mower Specs & Scores (Open Dataset)

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-blue.svg)](LICENSE)

An open, machine-readable dataset of **39 wire-free robot lawn mowers** across **9 brands**
(Dreame, EcoFlow, Ecovacs, Husqvarna, Mammotion, MOVA, Segway, Sunseeker, Worx), with cited specs, dated prices, and a transparent **0-5 BestRobotMower Score**
for every shipping model.

Compiled and computed by **[BestRobotMower.co](https://bestrobotmower.co/?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset)**, an independent robot-mower comparison site.
Every spec links back to the manufacturer source that proves it, and every score is a documented function of
those specs (no user polls, no opinion). Released under **[CC BY 4.0](LICENSE)** so you can use it freely
with attribution.

## 🔎 Explore it in your browser

**[Interactive spec explorer → yumaheymans.github.io/robot-lawn-mower-specs](https://yumaheymans.github.io/robot-lawn-mower-specs/)**
is the human-readable companion to the CSV/JSON below: a searchable, sortable table of all 70 models with the
0-5 score, specs, dated prices, and a link to each model's cited write-up.

**On the site:** the canonical, always-current version lives at
**[bestrobotmower.co/dataset](https://bestrobotmower.co/dataset?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset)**,
with a live machine-readable feed at
[`/api/dataset/mowers.json`](https://bestrobotmower.co/api/dataset/mowers.json) and
[`/api/dataset/mowers.csv`](https://bestrobotmower.co/api/dataset/mowers.csv) (CORS-open, refreshed with the site).
The files in this repo are a versioned snapshot for offline and reproducible use.

> **Why this exists:** there was no open, structured spec table for robot mowers anywhere. Robotics hobbyists,
> Home Assistant tinkerers, journalists, and buyers kept re-scraping the same manufacturer PDFs. This is that
> table, kept honest and cited.

## How to cite

CC BY 4.0 just asks for credit. If you use this data in an article, app, video, or paper, please attribute:

> BestRobotMower.co. *Robot Lawn Mower Specs & Scores* (open dataset, CC BY 4.0). https://bestrobotmower.co/dataset

GitHub's **"Cite this repository"** button (top of the sidebar) generates the same in APA or BibTeX from
[`CITATION.cff`](CITATION.cff). Each release is a fixed, citable snapshot of the data on a given date.

## Affiliate disclosure

BestRobotMower.co is an independent comparison site that earns affiliate commissions when readers buy through
some of its outbound links. **This dataset is the site's own compiled, cited data** (not scraped from third
parties, not fabricated), released under CC BY 4.0. The scores are computed from published specs and are not
influenced by affiliate relationships.

## What's inside

| File | Format | Rows |
|---|---|---|
| [`data/mowers.csv`](data/mowers.csv) | CSV (spreadsheet-friendly) | 70 |
| [`data/mowers.json`](data/mowers.json) | JSON (with dataset metadata) | 70 |
| [`CHANGELOG.md`](CHANGELOG.md) | What changed in each release | n/a |
| [`methodology.md`](methodology.md) | The full 0-5 scoring rubric | n/a |

- **70 shipping** models (on sale now, scored)
- Prices as of **2026-10-02**: 30 of the 70 headline prices are the brand store's live price read from its own
  product feed; the rest were checked by hand on the date in `price_as_of`.

## Schema

| Column | Description |
|---|---|
| `brand` | Manufacturer (e.g. Segway, Mammotion). |
| `model` | Full model name. |
| `status` | `shipping` (on sale now) or `announced` (revealed, not yet widely available). |
| `release_year` | Year the model shipped, or was announced. |
| `navigation_type` | Compact navigation class, e.g. `RTK GNSS`, `RTK + Vision`, `LiDAR + Vision`, `LiDAR + RTK + Vision`, `Vision`. |
| `navigation_detail` | One-line description of the positioning and boundary system. |
| `all_wheel_drive` | Whether the model is all-wheel drive (matters on slopes and rough ground). |
| `max_coverage_m2` | Manufacturer-rated maximum lawn area, in square metres. |
| `max_slope_pct` | Manufacturer-rated maximum slope, in percent grade. |
| `cutting_width_cm` | Cutting width, in cm. |
| `cut_height_min_mm` | Lowest cut height, in mm. |
| `cut_height_max_mm` | Highest cut height, in mm. |
| `battery_runtime_min` | Rated working time per charge, in minutes, where the maker states one. |
| `obstacle_avoidance` | The obstacle-detection system, from the maker's own description. |
| `price_usd` | Headline price in USD: the cheapest way to buy it from a tracked seller that is not sold out. |
| `price_provider` | The seller of that price. |
| `price_per_m2_usd` | price_usd divided by max_coverage_m2, a rough value indicator. |
| `bestrobotmower_score` | Transparent 0-5 BestRobotMower Score (shipping models). See the methodology below. |
| `score_navigation` | Sub-score, Navigation & mapping axis (weight 0.25). |
| `score_obstacle_avoidance` | Sub-score, Obstacle avoidance axis (weight 0.20). |
| `score_coverage` | Sub-score, Coverage axis (weight 0.20). |
| `score_slope` | Sub-score, Slope & terrain axis (weight 0.15). |
| `score_coverage_per_dollar` | Sub-score, Coverage per dollar axis (weight 0.20). |
| `model_page_url` | The model's page on BestRobotMower.co, with every figure's source. |
| `coverage_source_url` | Manufacturer source for the coverage figure. |
| `slope_source_url` | Manufacturer source for the slope figure. |
| `price_source_url` | The page that proves the price. |
| `summary` | One-line plain-language summary of the model. |
| `price_as_of` | Date the price was last confirmed (YYYY-MM-DD): the live store read, else the hand check. |
| `price_is_live` | `true` when price_usd is the brand store's live price read from its own product feed. |
| `in_stock` | The price seller's stock from its live feed: `true`, `false`, or empty when unknown. |

> The JSON rows also carry `slug`, the model's URL slug (the last segment of `model_page_url`).

> **Prices are dated.** Each row says when its price was confirmed (`price_as_of`) and whether it is a live
> brand-store price (`price_is_live`). Robot-mower prices move often; for today's price open the
> `model_page_url` or `price_source_url`.

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

| Model | Brand | Navigation | Max coverage | Max slope | AWD | Price | Score |
|---|---|---|---|---|---|---|---|
| [Yarbo Y40 Lawn Mower Pro](https://bestrobotmower.co/mowers/yarbo-y40-lawn-mower-pro?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Yarbo | RTK + Vision | 24,281 m² | 70% | No | $5,499 | **4.6** |
| [Dreame Roboticmower A3 AWD Pro](https://bestrobotmower.co/mowers/dreame-roboticmower-a3-awd-pro?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Dreame | LiDAR + Vision | 2,500 m² | 80% | Yes | $1,699.99 | **4.4** |
| [Lymow One Plus](https://bestrobotmower.co/mowers/lymow-one-plus?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Lymow | RTK + Vision | 7,001 m² | 100% | No | $3,199 | **4.4** |
| [Mammotion Luba 3 AWD](https://bestrobotmower.co/mowers/mammotion-luba-3-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | LiDAR + RTK + Vision | 3,000 m² | 80% | Yes | $2,109 | **4.4** |
| [MOVA LiDAX Ultra 3000 AWD](https://bestrobotmower.co/mowers/mova-lidax-ultra-3000-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | MOVA | LiDAR + Vision | 3,035 m² | 80% | Yes | $2,199 | **4.4** |
| [Ecovacs Goat A3000 LiDAR](https://bestrobotmower.co/mowers/ecovacs-goat-a3000-lidar?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | LiDAR + Vision | 3,035 m² | 50% | No | $1,910.76 | **4.3** |
| [Ecovacs Goat A3000 LiDAR PRO](https://bestrobotmower.co/mowers/ecovacs-goat-a3000-lidar-pro?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | LiDAR + Vision | 3,035 m² | 50% | No | $2,124.99 | **4.3** |
| [Mammotion Luba 2 AWD 5000](https://bestrobotmower.co/mowers/mammotion-luba-2-awd-5000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK GNSS | 5,000 m² | 80% | Yes | $2,299 | **4.3** |
| [MOVA LiDAX Ultra 2000](https://bestrobotmower.co/mowers/mova-lidax-ultra-2000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | MOVA | LiDAR + Vision | 2,000 m² | 45% | No | $1,099 | **4.3** |
| [MOVA LiDAX Ultra 2000 AWD](https://bestrobotmower.co/mowers/mova-lidax-ultra-2000-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | MOVA | LiDAR + Vision | 2,000 m² | 80% | Yes | $1,799 | **4.3** |
| [Segway Navimow X390](https://bestrobotmower.co/mowers/segway-navimow-x390?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK + Vision | 10,118 m² | 50% | No | $4,499 | **4.3** |
| [Ecovacs Goat A2000 LiDAR PRO](https://bestrobotmower.co/mowers/ecovacs-goat-a2000-lidar-pro?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | LiDAR + Vision | 2,023 m² | 50% | No | $1,399 | **4.2** |
| [Roborock RockMow X130H](https://bestrobotmower.co/mowers/roborock-rockmow-x130h?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Roborock | RTK + Vision | 4,000 m² | 80% | Yes | $2,499.98 | **4.2** |
| [Segway Navimow X350](https://bestrobotmower.co/mowers/segway-navimow-x350?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK + Vision | 6,070 m² | 50% | No | $2,799 | **4.2** |
| [Segway Navimow X4](https://bestrobotmower.co/mowers/segway-navimow-x4?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK + Vision | 4,047 m² | 84% | Yes | $2,499 | **4.2** |
| [Sunseeker X7 Plus Gen 2](https://bestrobotmower.co/mowers/sunseeker-x7-plus-gen-2?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Sunseeker | RTK + Vision | 6,070 m² | 70% | Yes | $3,299 | **4.2** |
| [Worx Landroid Vision Cloud 4WD WR344](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-4wd-wr344?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 4,000 m² | 83% | Yes | $2,471.70 | **4.2** |
| [Worx Landroid Vision Cloud 4WD WR346](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-4wd-wr346?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 6,000 m² | 83% | Yes | $3,699.99 | **4.2** |
| [Airseekers Tron](https://bestrobotmower.co/mowers/airseekers-tron?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Airseekers | RTK + Vision | 2,400 m² | 60% | No | $999 | **4.1** |
| [Airseekers Tron Plus](https://bestrobotmower.co/mowers/airseekers-tron-plus?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Airseekers | RTK + Vision | 4,000 m² | 60% | No | $2,099 | **4.1** |
| [Anthbot Genie 3000](https://bestrobotmower.co/mowers/anthbot-genie-3000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Anthbot | RTK + Vision | 3,000 m² | 45% | No | $899 | **4.1** |
| [Ecovacs Goat G1](https://bestrobotmower.co/mowers/ecovacs-goat-g1?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | LiDAR + Vision | 1,600 m² | 45% | No | $1,599 | **4.1** |
| [Mammotion Luba Mini 2 AWD](https://bestrobotmower.co/mowers/mammotion-luba-mini-2-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | LiDAR + Vision | 1,500 m² | 80% | Yes | $1,699 | **4.1** |
| [Roborock RockMow X120H LiDAR](https://bestrobotmower.co/mowers/roborock-rockmow-x120h-lidar?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Roborock | LiDAR + Vision | 2,000 m² | 80% | Yes | $2,299 | **4.1** |
| [Segway Navimow X330](https://bestrobotmower.co/mowers/segway-navimow-x330?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK + Vision | 4,047 m² | 50% | No | $2,299 | **4.1** |
| [Airseekers Tron SE](https://bestrobotmower.co/mowers/airseekers-tron-se?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Airseekers | RTK + Vision | 1,500 m² | 60% | No | $855 | **4.0** |
| [Dreame A3 AWD](https://bestrobotmower.co/mowers/dreame-a3-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Dreame | LiDAR + Vision | 1,000 m² | 80% | Yes | $1,399.99 | **4.0** |
| [MOVA LiDAX Ultra 1000](https://bestrobotmower.co/mowers/mova-lidax-ultra-1000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | MOVA | LiDAR + Vision | 1,000 m² | 45% | No | $949 | **4.0** |
| [Roborock RockMow X115H](https://bestrobotmower.co/mowers/roborock-rockmow-x115h?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Roborock | RTK + Vision | 1,500 m² | 80% | Yes | $1,499.98 | **4.0** |
| [Segway Navimow i2 LiDAR](https://bestrobotmower.co/mowers/segway-navimow-i2-lidar?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | LiDAR + Vision | 1,497 m² | 45% | No | $1,599 | **4.0** |
| [Sunseeker X5](https://bestrobotmower.co/mowers/sunseeker-x5?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Sunseeker | RTK + Vision | 2,000 m² | 60% | Yes | $1,499 | **4.0** |
| [Sunseeker X7 Gen 2](https://bestrobotmower.co/mowers/sunseeker-x7-gen-2?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Sunseeker | RTK + Vision | 3,035 m² | 70% | Yes | $2,599 | **4.0** |
| [Worx Landroid Vision Cloud 4WD WR342](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-4wd-wr342?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 2,000 m² | 83% | Yes | $2,069.99 | **4.0** |
| [Worx Landroid Vision Cloud WR340](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-wr340?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 4,000 m² | 30% | No | $2,069.99 | **4.0** |
| [Anthbot M9](https://bestrobotmower.co/mowers/anthbot-m9?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Anthbot | RTK + Vision | 1,000 m² | 45% | No | $699 | **3.9** |
| [Ecovacs Goat A2500 RTK](https://bestrobotmower.co/mowers/ecovacs-goat-a2500-rtk?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | RTK + Vision | 2,023 m² | 50% | No | $1,748.33 | **3.9** |
| [Ecovacs Goat O1000 LiDAR PRO](https://bestrobotmower.co/mowers/ecovacs-goat-o1000-lidar-pro?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | LiDAR + Vision | 1,012 m² | 45% | No | $1,255.90 | **3.9** |
| [Sunseeker S4](https://bestrobotmower.co/mowers/sunseeker-s4?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Sunseeker | LiDAR + Vision | 1,000 m² | 42% | No | $1,299.99 | **3.9** |
| [Worx Landroid Vision Cloud WR320](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-wr320?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 2,000 m² | 30% | No | $1,369.85 | **3.9** |
| [Anthbot Genie 1000](https://bestrobotmower.co/mowers/anthbot-genie-1000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Anthbot | RTK + Vision | 1,000 m² | 45% | No | $799 | **3.8** |
| [EcoFlow Blade](https://bestrobotmower.co/mowers/ecoflow-blade?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | EcoFlow | RTK GNSS | 2,800 m² | 27% | No | $2,899 | **3.8** |
| [Ecovacs Goat O1000 RTK](https://bestrobotmower.co/mowers/ecovacs-goat-o1000-rtk?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | RTK + Vision | 799 m² | 45% | No | $664 | **3.8** |
| [Mammotion Yuka Mini 2](https://bestrobotmower.co/mowers/mammotion-yuka-mini-2?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | LiDAR + Vision | 1,000 m² | 45% | No | $1,399 | **3.8** |
| [Roborock RockNeo Q110H](https://bestrobotmower.co/mowers/roborock-rockneo-q110h?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Roborock | RTK + Vision | 1,000 m² | 45% | No | $799.98 | **3.8** |
| [Sunseeker X3 Plus](https://bestrobotmower.co/mowers/sunseeker-x3-plus?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Sunseeker | RTK + Vision | 1,200 m² | 30% | No | $999 | **3.8** |
| [Worx Landroid Vision Cloud WR320.1](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-wr320-1?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 2,000 m² | 30% | No | $1,799.99 | **3.8** |
| [Anthbot Genie 600e](https://bestrobotmower.co/mowers/anthbot-genie-600e?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Anthbot | RTK + Vision | 600 m² | 45% | No | $699 | **3.7** |
| [Anthbot M5 LiDAR](https://bestrobotmower.co/mowers/anthbot-m5-lidar?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Anthbot | LiDAR + Vision | 500 m² | 45% | No | $799 | **3.7** |
| [Anthbot N8](https://bestrobotmower.co/mowers/anthbot-n8?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Anthbot | RTK + Vision | 1,500 m² | 45% | No | $1,699 | **3.7** |
| [Ecovacs Goat O1200](https://bestrobotmower.co/mowers/ecovacs-goat-o1200?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Ecovacs | RTK + Vision | 1,200 m² | 45% | No | $1,499 | **3.7** |
| [Mammotion Yuka 1500](https://bestrobotmower.co/mowers/mammotion-yuka-1500?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK + Vision | 1,500 m² | 45% | No | $1,799 | **3.7** |
| [Segway Navimow H2](https://bestrobotmower.co/mowers/segway-navimow-h2?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | LiDAR + RTK + Vision | 1,012 m² | 45% | No | $1,799 | **3.7** |
| [Segway Navimow i110N](https://bestrobotmower.co/mowers/segway-navimow-i110n?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK GNSS | 1,012 m² | 30% | No | $1,099 | **3.7** |
| [Worx Landroid Vision Cloud WR310](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-wr310?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 1,000 m² | 30% | No | $968.98 | **3.7** |
| [Anthbot M5](https://bestrobotmower.co/mowers/anthbot-m5?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Anthbot | RTK + Vision | 500 m² | 45% | No | $649 | **3.6** |
| [Dreame Roboticmower A1](https://bestrobotmower.co/mowers/dreame-roboticmower-a1?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Dreame | LiDAR + Vision | 2,000 m² | 45% | No | $2,099 | **3.6** |
| [Mammotion Luba 2 AWD 1000](https://bestrobotmower.co/mowers/mammotion-luba-2-awd-1000?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK GNSS | 1,000 m² | 80% | Yes | $1,699 | **3.6** |
| [Mammotion Yuka Mini](https://bestrobotmower.co/mowers/mammotion-yuka-mini?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Mammotion | RTK + Vision | 809 m² | 50% | No | $1,099 | **3.6** |
| [Worx Landroid Vision Cloud](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 1,000 m² | 30% | No | $1,199.99 | **3.6** |
| [Worx Landroid Vision WR220](https://bestrobotmower.co/mowers/worx-landroid-vision-wr220?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | Vision | 2,023 m² | 30% | No | $1,572.72 | **3.6** |
| [Segway Navimow i2 AWD](https://bestrobotmower.co/mowers/segway-navimow-i2-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK + Vision | 607 m² | 45% | Yes | $999 | **3.5** |
| [Sunseeker V3](https://bestrobotmower.co/mowers/sunseeker-v3?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Sunseeker | Vision | 600 m² | 42% | No | $599.99 | **3.5** |
| [Worx Landroid Vision Cloud 4WD WR341](https://bestrobotmower.co/mowers/worx-landroid-vision-cloud-4wd-wr341?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Worx | RTK + Vision | 1,000 m² | 83% | Yes | $1,880.54 | **3.5** |
| [Husqvarna Automower 440 iQ](https://bestrobotmower.co/mowers/husqvarna-automower-440-iq?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Husqvarna | RTK GNSS | 8,094 m² | 45% | No | $4,299.99 | **3.4** |
| [Segway Navimow i105E](https://bestrobotmower.co/mowers/segway-navimow-i105e?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Segway | RTK GNSS | 506 m² | 30% | No | $799 | **3.4** |
| [MOVA LiDAX Pro 800](https://bestrobotmower.co/mowers/mova-lidax-pro-800?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | MOVA | LiDAR + Vision | 800 m² | 45% | No | $849 | **3.3** |
| [eufy E15](https://bestrobotmower.co/mowers/eufy-e15?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | eufy | Vision | 800 m² | 32% | No | $1,299.99 | **3.2** |
| [Husqvarna Automower 420 iQ](https://bestrobotmower.co/mowers/husqvarna-automower-420-iq?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Husqvarna | RTK GNSS | 4,047 m² | 45% | No | $3,299.99 | **3.2** |
| [Husqvarna Automower 435 iQ AWD](https://bestrobotmower.co/mowers/husqvarna-automower-435-iq-awd?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Husqvarna | RTK GNSS | 3,642 m² | 70% | Yes | $4,999.99 | **3.1** |
| [Husqvarna Automower 410 iQ](https://bestrobotmower.co/mowers/husqvarna-automower-410-iq?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset) | Husqvarna | RTK GNSS | 2,023 m² | 45% | No | $2,599.99 | **3.0** |

Prices as of 2026-10-02; each row's own date is in `price_as_of`.

## Using & citing

Free to use, adapt, and redistribute under CC BY 4.0 with attribution. Suggested citation:

> Robot Lawn Mower Specs & Scores dataset, BestRobotMower.co, https://bestrobotmower.co, 2026-10-02. Licensed CC BY 4.0.

If you build something with this (a comparison tool, a Home Assistant integration, a chart), open an issue or PR
and it can be linked here.

## Updating

Specs and prices drift. This snapshot was compiled **2026-09-29** (prices as of **2026-09-29**).
The live, continuously-updated version of every figure here is on the model pages at
[BestRobotMower.co](https://bestrobotmower.co/mowers?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset).

---

Data and scores © BestRobotMower.co, released under [CC BY 4.0](LICENSE). Built and maintained alongside
[bestrobotmower.co](https://bestrobotmower.co/?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset): independent robot-mower comparisons covering specs, prices, and navigation.
