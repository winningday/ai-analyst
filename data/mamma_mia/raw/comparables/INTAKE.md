# Comparable Productions — Intake Checklist

Source: **Tessitura Analytics / Tessitura sales reports** for prior Ahmanson
productions. Used to benchmark Mamma Mia!'s pace independently — we don't
trust the built-in Tessitura Analytics sales-curve comparison until we
verify it.

There's a working set of these reports already pulled for prior shows in
`C:\Users\mgoodman\OneDrive - Center Theatre Group of Los Angeles\Documents\Code\sales\data\`.
Copy the relevant files here (don't symlink — keep this folder
self-contained) and add fresh pulls for any comparable not yet covered.

---

## Choose comparables (fill in)

Pick 3–5 prior Ahmanson productions that are reasonable analogs. Criteria:

- Same venue (Ahmanson) — capacity and audience overlap matter
- Similar genre / scale (commercial musical preferred)
- Recent enough that ticketing behavior is comparable (post-COVID; ideally
  last 2–3 seasons)
- Has a complete sales history (full run from on-sale to closing)

> **Comparables for this analysis:**
> 1. `__________`
> 2. `__________`
> 3. `__________`
> 4. `__________`
> 5. `__________`

---

## Files needed (per comparable)

Match the formats already in use in the `Code\sales\data\` folder so the
existing helpers can read them. Filenames here should be production-tagged.

### 1. Daily sales accumulation by performance

**File:** `comparables_daily_accumulation_{prod_slug}.csv`

Source format: `daily_sales_accumulation_by_performance.csv`

| Field | Notes |
|---|---|
| `sale_date` | The day tickets were sold |
| `perf_id` | Tessitura performance ID |
| `perf_code_short` | Short code |
| `production_season` | Production name |
| `perf_date` | Performance date |
| `tickets_sold` | Cumulative or daily — confirm and label clearly |
| `revenue` | Same convention as tickets_sold |

Used to build **% sold by N days before performance** curves and compare
Mamma Mia's curve against each comparable.

### 2. Performance-level historical (final outcomes)

**File:** `comparables_performance_level_{prod_slug}.csv`

Source format: `performance-level_historical.csv`

| Field | Notes |
|---|---|
| `perf_id` | |
| `perf_code_short` | |
| `production_season` | |
| `perf_date` | |
| `perf_time` | |
| `st_final_sold` | Single-ticket final sold |
| `total_tickets_sold` | All ticket types final |
| `final_capacity` | |
| `final_revenue` | |
| `seats_available` | |
| `holds` | |

Used as the **ground-truth final** to validate any forecasting model on
out-of-sample data before applying it to Mamma Mia's open run.

### 3. (Optional) Performance Sales Analysis snapshot

If we want zone × price-type benchmarking, pull the same Performance Sales
Analysis report (see `tessitura/INTAKE.md` pull #3) for one or two
comparables at a similar point in their run. Save as
`comparables_perf_sales_analysis_{prod_slug}_{date}.csv`.

---

## Naming

`prod_slug` = lowercase, dashes, no special chars. Examples:

- `here-lies-love`
- `paranormal-activity`
- `2-22-a-ghost-story`
- `the-secret-garden`

---

## Anomalies / notes

> Log differences across comparable productions here (different price tiers,
> different on-sale lead times, COVID-era weirdness, etc.).

-
-
