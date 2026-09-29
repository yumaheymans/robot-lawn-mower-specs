# Changelog

Each release is a dated, citable snapshot. Robot-mower prices move often; the live, always-current version is at [bestrobotmower.co/dataset](https://bestrobotmower.co/dataset?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset).

## v2026.09.29 (2026-09-29)

**23 to 39 models, still 9 brands.** Prices as of 2026-09-29; 22 of the 39 headline prices are the brand store's live price read from its own product feed.

### Added (16)

Ecovacs: Goat A3000 LiDAR PRO, Goat O1000 LiDAR PRO; MOVA: LiDAX Pro 800, LiDAX Ultra 2000, LiDAX Ultra 2000 AWD; Mammotion: Luba 3 AWD, Luba Mini 2 AWD, Yuka Mini 2; Segway: Navimow H2, Navimow X350, Navimow X4, Navimow i2 AWD, Navimow i2 LiDAR; Sunseeker: S4, V3, X5.

### Corrected

- **Segway Navimow X330:** rated coverage 3,000 m² to 4,047 m² (1 acre, per Segway's current product page).
- **Segway Navimow X390:** on sale in the US since April 2025 (release year 2026 to 2025); now scored (4.6) instead of unscored.
- **Ecovacs Goat A3000 LiDAR:** navigation is dual LiDAR plus vision, not RTK plus vision; on sale since 2025 (release year 2026 to 2025); now scored (4.3).
- **Mammotion Luba 2 AWD 5000:** the US store now sells the 5000HX only, so the cut height is the H deck (55 to 100 mm).
- **Worx Landroid Vision WR220:** price $999.99 to $2,499.99 (Worx store); the earlier figure was stale.
- **Husqvarna Automower 410 iQ:** price $2,999 to $2,599.99.
- Other price moves read from the brand stores: Dreame A3 AWD Pro $2,249.99 to $1,699.99, Dreame A3 AWD $1,599.99 to $1,399.99, MOVA LiDAX Ultra 3000 AWD $2,399 to $2,199, Luba 2 AWD 5000 $2,899 to $2,299 (Amazon; $2,999 at Mammotion), Sunseeker X3 Plus $999 to $899.99, Goat A2000 LiDAR PRO $1,399 to $1,452.
- **Scores** were recomputed on the current catalog and prices (the coverage and coverage-per-dollar axes are scored against the field, and prices moved): 15 of the 21 previously scored models moved, by 0.1 to 0.2 except the Worx Landroid Vision WR220 (4.0 to 3.5, from its corrected price). The rubric is unchanged ([`methodology.md`](methodology.md)).

### Schema

The files now match the live API at [`/api/dataset/mowers.json`](https://bestrobotmower.co/api/dataset/mowers.json) exactly, so a snapshot and the live feed read the same way.

- **Removed:** `coverage_tiers`, `cutting_spec`, `lawn_size_class`, `price_snapshot_usd`, `price_snapshot_provider`, `price_snapshot_date`.
- **Added:** `cutting_width_cm`, `cut_height_min_mm`, `cut_height_max_mm`, `battery_runtime_min`, `obstacle_avoidance`, `price_usd`, `price_provider`, `price_as_of`, `price_is_live`, `in_stock`.
- `data/mowers.json` is now `{name, description, license, ..., rows: [...]}` (it was `{dataset, ..., models: [...]}`).

## v2026.08.24 (2026-08-24)

First release: 23 models (21 shipping, 2 announced), 9 brands, cited specs, dated price snapshots and the 0-5 score.
