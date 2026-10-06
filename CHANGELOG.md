# Changelog

Each release is a dated, citable snapshot. Robot-mower prices move often; the live, always-current version is at [bestrobotmower.co/dataset](https://bestrobotmower.co/dataset?utm_source=github&utm_medium=readme&utm_campaign=mower-dataset).

## v2026.10.05 (2026-10-05)

**Amazon prices are no longer quoted.** Prices as of 2026-10-05; 44 of the 76 headline prices are the brand store's live price read from its own product feed.

### Changed

- **No Amazon prices.** Amazon shows its own current price and stock on each listing, so the dataset no longer quotes them. `price_usd` is now the cheapest price we quote from a brand store or retailer that is not sold out. Releases up to v2026.10.03 quoted hand-checked Amazon prices: use this release instead.
- **10 models have an empty `price_usd`**, because Amazon is the only seller we track that is not sold out of them: Mammotion Yuka 1500, Ecovacs Goat A3000 LiDAR, Worx Landroid Vision WR220, Roborock RockNeo Q110H, Roborock RockMow X115H, Roborock RockMow X130H, Roborock RockMow X120H LiDAR, Ecovacs Goat A2500 RTK, Worx Landroid Vision Cloud WR310, Worx Landroid Vision Cloud WR320. Each row's `model_page_url` leads to the model's page, which links the Amazon listing.
- **Where Amazon had been the cheapest seller**, `price_usd`, `price_provider` and the price-derived score axis now come from the next seller (usually the brand's own store), so some headline prices are higher than in v2026.10.03 and some 0-5 scores moved by 0.1 to 0.3. The six picks on the site are unchanged.
- **Store prices are read daily** (they were read every three days), so `price_as_of` on a live price is at most a day old.

## v2026.10.03 (2026-10-03)

**70 to 76 models.** Prices as of 2026-10-03; 31 of the 76 headline prices are the brand store's live price read from its own product feed.

### Added (6)

Dreame: Roboticmower A3 AWD Pro 3500, Roboticmower A3 AWD Pro 5000, A3 AWD 2000; Mammotion: Luba 3 AWD 5000; Segway: Navimow X450, Navimow H220.

Each is another size tier of a model already in the dataset. Tiers are separate rows because they differ in rated area, battery and price, which are the figures a buyer compares; the earlier rows kept one tier per store listing, so the larger tiers (the answers for a 1-acre lawn) were missing.

- **Dreame:** Dreame publishes no mowing time per charge for any A3 tier, so `battery_runtime_min` is empty for them. Dreame's store labels the Pro 5000 as 1.20 acres; its US manual and the 5,000 m² rating give 1.24.
- **Segway Navimow X450:** 6,070 m² (1.5 acres) is Segway's US rating; its EU and Australian X450 is rated 5,000 m². Sold out at Segway's own store on 2026-10-03.

### Corrected

- **Dreame A3 AWD (1000):** noise 62.8 to 70.8 dB, the sound power level (LWA) every other row uses. Dreame's page advertises 62.8 dB, which is the sound pressure level (LpA).
- **The README introduction** said 39 models across 9 brands since v2026.09.29 while the data said otherwise: the script that rewrites it had stopped matching its own text. It now states the current counts and fails loudly if a rewrite misses.

## v2026.10.02 (2026-10-02)

**55 to 70 models, 14 to 15 brands.** Prices as of 2026-10-02; 30 of the 70 headline prices are the brand store's live price read from its own product feed.

### Added (15)

Ecovacs: Goat A2500 RTK, Goat O1000 RTK; Husqvarna: Automower 420 iQ, Automower 440 iQ; Sunseeker: X7 Gen 2, X7 Plus Gen 2; Worx: Landroid Vision Cloud WR310, WR320, WR320.1, WR340, Landroid Vision Cloud 4WD WR341, WR342, WR344, WR346; Yarbo: Y40 Lawn Mower Pro (new brand).

Worx is listed by part number because the parts differ: the `.1` parts add the Cut-to-Zero edge module. Worx's own US store sells the WR310.1, WR320.1, WR340 and the four 4WD parts; Amazon sells the original WR310 and WR320, which lack the module.

Where a maker's own figures disagree, the dataset takes the conservative one and the model's page says so:

- **Worx Landroid Vision Cloud 4WD:** slope 83%. Worx's spec table says 84% (40°) and its product copy 83%. Worx's manuals also advise against slopes over 15° with the Cut-to-Zero module fitted, which it is as standard on the 4WD parts, the `.1` parts and the WR340.
- **Worx runtimes** come from Worx's own comparison chart on its Amazon listings (its US product pages and manuals publish none). The chart does not cover the WR310.1 or WR320.1, so their `battery_runtime_min` is empty.

### Corrected

- **Worx Landroid Vision Cloud:** this row is part WR310.1, the quarter-acre part Worx's US store sells: coverage 1,012 to 1,000 m², slope 35% to 30%, runtime removed, release year 2024 to 2026. Its earlier figures mixed in other parts' claims (4G, a 60-minute runtime).
- **Husqvarna Automower 435 iQ AWD:** coverage 5,261 to 3,642 m² (Husqvarna rates it at 0.9 acre). Its price now comes from Husqvarna's store ($4,999.99), since Amazon does not sell it new.
- **Worx Landroid Vision WR220:** out of stock at Worx; the headline price is a third-party seller on Amazon ($1,572.72).
- **Ecovacs Goat A2000 LiDAR PRO:** $1,452 to $1,399 (Ecovacs store sale; list $1,999.99).
- **Ecovacs Goat A3000 LiDAR, A3000 LiDAR PRO and O1000 LiDAR PRO:** Amazon prices added; Amazon is now the cheapest for each.
- **EcoFlow Blade:** EcoFlow's US store no longer sells it. The row keeps the last list price EcoFlow published (on its Australian store), out of stock.
- **Scores** were recomputed against the larger field (the coverage and coverage-per-dollar axes are scored against the whole field): 34 earlier models moved by 0.1 to 0.2. The rubric is unchanged.

## v2026.10.01 (2026-10-01)

**39 to 55 models, 9 to 14 brands.** Prices as of 2026-10-01; 30 of the 55 headline prices are the brand store's live price read from its own product feed.

### Added (16)

Airseekers: Tron, Tron Plus, Tron SE; Anthbot: Genie 600e, Genie 1000, Genie 3000, M5, M5 LiDAR, M9, N8; eufy: E15; Lymow: One Plus; Roborock: RockMow X115H, RockMow X120H LiDAR, RockMow X130H, RockNeo Q110H.

Where a maker's own figures disagree, the dataset takes the conservative one and the model's page says so:

- **Anthbot Genie 600e, 1000 and 3000:** coverage from Anthbot's spec table and manual (600, 1,000 and 3,000 m²), not the larger figures on its product page.
- **Airseekers Tron family:** slope is the 60% working (mowing) grade from Airseekers' spec table, not the 65% climbing headline.
- **Lymow One Plus:** Lymow rates coverage per day (1.73 acres with the 10A charger, a lab maximum), not as a maximum lawn size.
- **Roborock RockMow X115H and X130H:** `battery_runtime_min` is empty because Roborock's spec page and its US manual give different runtimes.
- **Roborock:** sold in the US through Amazon only, so its prices are Amazon's regular prices; the RockMow X120H LiDAR is out of stock there (`in_stock` false).

### Corrected

- **MOVA LiDAX Pro 800:** score 4.1 to 3.3. Gizmodo's hands-on review saw its obstacle avoidance fail, so the score no longer credits its camera avoidance ([methodology](methodology.md)).
- **Scores** were recomputed against the larger field (the coverage and coverage-per-dollar axes are scored against the whole field): 26 more of the 39 earlier models moved, by 0.1 to 0.2. The rubric is unchanged.
- Price moves read from the stores: Sunseeker S4 $999.99 to $1,299.99, Sunseeker X3 Plus $899.99 to $999 (Amazon), MOVA LiDAX Ultra 1000 $999 to $949.

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
