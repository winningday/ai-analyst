# Mamma Mia! — Sales Drop & Run Forecast Analysis (Raw Data Intake)

This folder holds raw exports for analyzing the Fri–Sun sales drop on the
Mamma Mia! run **and** for forecasting where the run lands vs. goal.

## Analysis context

- **Show:** Mamma Mia! (Ahmanson)
- **Issue:** Strong Mon/Tue sales (digital ads + Wordfly email blast Mon).
  Pacing implied ~77,000 for the week. Sales dropped substantially Fri/Sat/Sun.
- **Working hypothesis:** Suspect we're behind pace for the run. Tessitura
  Analytics' built-in sales-curve comparison may be misleading — we'll do an
  independent benchmark against comparable Ahmanson productions.

## Analytical goals

1. **Root-cause the Fri–Sun drop.** Was it demand pulled forward by the Mon
   email blast, ad pressure dropping, audience fatigue, a tracking break, or
   a price change?
2. **Forecast end-of-run final numbers** (tickets + revenue) with a confidence
   range, by performance and aggregated for the run.
3. **Build a weekly pace target.** Given the goal, how many tickets / how much
   revenue do we need per week from now until close? Flag the gap if behind.
4. **Benchmark against comparable Ahmanson runs.** Use prior productions'
   sales-accumulation curves to validate (or refute) the Tessitura sales-curve
   comparison. Treat Tessitura's comparison as "to be verified," not truth.
5. **Quantify dynamic-pricing impact.** Did price-level changes coincide with
   sales lifts or drops? Identify zones where the pricing rule may be hurting.

## Please fill in before analysis starts

> Edit this section once with the specifics so the analysis can anchor on real
> dates, the right comparison set, and the run goal.

- **Drop week (Mon → Sun):** `____-__-__` to `____-__-__`
- **Mamma Mia! run dates (first → last performance):** `____-__-__` to `____-__-__`
- **Mamma Mia! Tessitura season ID:** `____` (e.g., `209` for 2024-2025 CTG Season)
- **Run revenue goal / ticket goal:** `$________` / `_____ tickets`
  (and, if separate, the **paid-attendance** goal)
- **Comparable Ahmanson productions for benchmarking:**
  `__________` (e.g., recent musicals at the same venue, similar genre/scale)
- **Known caveats:**
  - Are comps included in revenue? `yes / no`
  - Are refunds netted into the sales figure? `yes / no`
  - Any campaign / promo changes mid-week? `__________`
  - Any dynamic-pricing rule changes during the run? `__________`

## Source folders

| Folder | Source | Owner |
|---|---|---|
| `tessitura/` | Sales, inventory, performance sales analysis (Tessitura Analytics CSV exports) | Internal |
| `dynamic_pricing/` | Daily-updated price-change log from the pricing system | Internal |
| `comparables/` | Sales / accumulation history for prior comparable Ahmanson productions | Internal |
| `google_analytics/` | Traffic, acquisition, on-site funnel (GA CSV exports) | Internal |
| `email_wordfly/` | Email campaign metrics (Wordfly → Looker Studio merge → CSV) | Internal |
| `digital_ads/` | Paid media spend & performance (CSV from agency) | External agency |

Each subfolder has its own `INTAKE.md` listing the exact pulls needed.

## File naming convention

```
{source}_{report}_{start}_to_{end}.csv

tessitura_sales_2026-02-01_to_2026-04-29.csv
tessitura_inventory_snapshot_2026-04-29.csv
tessitura_perf_sales_analysis_2026-04-29.csv
dynamic_pricing_changes_2026-04-29.csv
comparables_daily_accumulation_ahmanson.csv
ga_acquisition_2026-02-01_to_2026-04-29.csv
ga_funnel_2026-02-01_to_2026-04-29.csv
wordfly_email_2026-02-01_to_2026-04-29.csv
ads_meta_2026-02-01_to_2026-04-29.csv
ads_google_2026-02-01_to_2026-04-29.csv
```

For files that are inherently snapshots (inventory, perf-sales analysis,
dynamic pricing dump), use the date the snapshot was taken.

## Time window

Pull at least **12 weeks** of history (drop week + 11 prior weeks) for every
sales/marketing source. For comparables, pull the **full run** of each
comparable production (so we can build full sales-accumulation curves). For
dynamic pricing, pull from the first price load through today.

## Data hygiene

- Keep raw CSVs untouched in `raw/`. Do not edit them in Excel — it can
  corrupt date and number formats. If you must inspect, use a viewer.
- If a file contains customer PII (names, emails, addresses), **redact or
  drop those columns before placing the file here.** We don't need PII for
  this analysis; aggregates and anonymized IDs are sufficient.
- Note any anomalies (missing days, partial pulls, schema changes) in the
  source's `INTAKE.md`.

## What happens after files land

1. I'll register this dataset in `.knowledge/datasets/mamma_mia/manifest.yaml`.
2. Run `/data-profiling` to inspect schemas, distributions, completeness.
3. Run a Source Tie-Out (pandas vs. DuckDB) on the sales totals.
4. Frame the question, hypothesize, analyze, validate, report.
5. Build the pace tracker and end-of-run forecast (with comparable-curve
   benchmark) as the central deliverables.
