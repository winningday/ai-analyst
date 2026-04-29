# Mamma Mia! — Sales Drop Analysis (Raw Data Intake)

This folder holds raw exports for analyzing the Fri–Sun sales drop on the
Mamma Mia! run.

## Analysis context

- **Show:** Mamma Mia!
- **Issue:** Strong Mon/Tue sales (digital ads + Wordfly email blast Mon).
  Pacing implied ~77,000 for the week. Sales dropped substantially Fri/Sat/Sun.
- **Goal:** Identify the root cause of the late-week drop and quantify
  forecast vs. actual gap.

## Please fill in before analysis starts

> Edit this section once with the specifics so the analysis can anchor on real
> dates and the right comparison set.

- **Drop week (Mon → Sun):** `____-__-__` to `____-__-__`
- **Mamma Mia! run dates (first → last performance):** `____-__-__` to `____-__-__`
- **Venue / market:** `__________`
- **Prior Mamma Mia! runs to compare against (yes/no, dates):** `__________`
- **Comparable productions for benchmarking:** `__________`
- **Known caveats:**
  - Are comps included in revenue? `yes / no`
  - Are refunds netted into the sales figure? `yes / no`
  - Any campaign / promo changes mid-week? `__________`

## Source folders

| Folder | Source | Owner |
|---|---|---|
| `tessitura/` | Sales + inventory (Tessitura Analytics, CSV export) | CISO / internal |
| `google_analytics/` | Traffic, acquisition, on-site funnel (GA CSV exports) | Internal |
| `email_wordfly/` | Email campaign metrics (Wordfly → Looker Studio merge → CSV) | Internal |
| `digital_ads/` | Paid media spend & performance (CSV from agency) | External agency |

Each subfolder has its own `INTAKE.md` listing the exact pulls needed.

## File naming convention

```
{source}_{report}_{start}_to_{end}.csv

tessitura_sales_2026-02-01_to_2026-04-29.csv
tessitura_inventory_snapshot_2026-04-29.csv
ga_acquisition_2026-02-01_to_2026-04-29.csv
ga_funnel_2026-02-01_to_2026-04-29.csv
wordfly_email_2026-02-01_to_2026-04-29.csv
ads_meta_2026-02-01_to_2026-04-29.csv
ads_google_2026-02-01_to_2026-04-29.csv
```

## Time window

Pull at least **12 weeks** of history (drop week + 11 prior weeks) for every
source. If a prior Mamma Mia! run exists, pull that too — it's the cleanest
comparison.

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
