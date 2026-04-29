# Tessitura — Intake Checklist

Source: **Tessitura Analytics** (CISO platform). CSV exports.

Two pulls needed.

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

## Anomalies / notes

> Log anything weird you notice during the pull (missing days, schema
> differences across exports, odd values).

-
-
