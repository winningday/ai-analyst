# Tessitura — Intake Checklist

Source: **Tessitura Analytics** (CISO platform). CSV exports.

Three pulls needed.

---

## 1. Daily sales — transaction grain

**File:** `tessitura_sales_{start}_to_{end}.csv`

One row per ticket sold (or per order line). 12 weeks history minimum.
Filter to Mamma Mia! production, but if it's easier to export the full
catalog and we'll filter in code, that works too.

**Required columns** (use closest Tessitura equivalent):

| Field | Notes |
|---|---|
| `transaction_datetime` | When the order was placed (date + time if possible) |
| `performance_date` | The date of the show being attended |
| `performance_time` | Curtain time (matinee vs. evening matters) |
| `production` | "Mamma Mia!" — keep all shows for context |
| `price_type` | Full, subscriber, group, comp, student, etc. |
| `price_zone` / `section` | Seating zone or price tier |
| `seats_sold` | Quantity (if a row = an order line) |
| `gross_revenue` | Pre-discount revenue |
| `net_revenue` | Post-discount, post-fees |
| `discount_code` | Promo code if used |
| `channel` | web / phone / box office |
| `customer_type` | new / repeat / subscriber if available |
| `order_id` | For dedup and validation |

**Important:** distinguish **transaction date** (when bought) from
**performance date** (which show). Both must be present.

---

## 2. Inventory snapshot

**File:** `tessitura_inventory_snapshot_{date}.csv`

Remaining seats by performance × price zone. Ideally **one snapshot per day**
across the drop week (so we can see when tiers sold out). If only a current
snapshot is possible, that's still useful.

**Required columns:**

| Field | Notes |
|---|---|
| `snapshot_date` | When the snapshot was taken |
| `performance_date` | Show date |
| `performance_time` | Curtain time |
| `price_zone` | Seating zone |
| `seats_available` | Currently for sale |
| `seats_sold` | Already sold |
| `seats_held` | Held / unavailable (comps, holds, kills) |
| `capacity` | Total seats in zone (sanity check) |

---

## 3. Performance Sales Analysis (zone × price-type cross-tab)

**File:** `tessitura_perf_sales_analysis_{date}.csv`

This report breaks every performance into Available / Held / Sold counts by
**price zone × price type** in one export. It complements pull #2 by giving
the price-type detail (full, subscriber, group, comp, etc.) per zone, which
is critical for diagnosing where the drop hit.

We already have one snapshot in this folder
(`20260429PerformanceSalesAnalysis.csv`, 3,937 rows, all Mamma Mia! perfs).
Going forward we want **a fresh snapshot per day** through the run so we can
build sales curves by zone × price type.

**Tessitura report parameters** (Mamma Mia run — fill in season ID & dates
from the run data in the README):

- **Report:** Performance Sales Analysis
- **Season ID:** `____` (Mamma Mia's season — e.g., `209` was 2024-2025)
- **Performance Start Date:** Mamma Mia first performance
- **Performance End Date:** Mamma Mia last performance
- **Save / export as:** `Email-CSV (hdr)`
- **Columns:** `Price Zones`
- **Rows:** `Price Type`
- **Show unpaid seats:** `Separate Detail Row`
- **Include resold seats:** `Yes`

**Schema** (confirmed from existing pull):

| Field | Notes |
|---|---|
| `perf_no` | Tessitura performance ID |
| `day_of_week` | |
| `perf_date` | Datetime of performance (e.g., `6/23/2026 7:30:00 PM`) |
| `perf_code` | Short code (e.g., `MAM0623TUE`) |
| `perf_description` | Production name |
| `row_group` | `Available` / `Held` / `Sold` (and unpaid as separate row) |
| `price_type` | Empty for Available/Held rows; set for Sold |
| `price_type_description` | |
| `ticket_count` | Count of seats in this bucket |
| `ticket_price` | Price paid (0 for Available/Held) |
| `ticket_amount` | Revenue (0 for Available/Held) |
| `column_group` | Zone label with base price (e.g., `BalC @ 75.00`) |
| `base_price` | Numeric base price for the zone |
| `zone_description` | Clean zone code (e.g., `BalC`, `MezA`, `Prem`) |

**Optional second pull — comparable production:** Run the same report for one
or two comparable Ahmanson productions (see `comparables/INTAKE.md`) so we
can benchmark sold-vs-available curves zone-for-zone, not just totals.

---

## Anomalies / notes

> Log anything weird you notice during the pull (missing days, schema
> differences across exports, odd values).

-
-
