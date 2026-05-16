# Dynamic Pricing — Intake Checklist

Source: **Dynamic pricing system** (the daily-updated CSV of every price
change loaded into Tessitura). One giant file, refreshed daily.

This is the **price-change log** — every (show × price level × performance)
gets a new row each time the price moves, with enactment timestamps. We need
this to test whether price changes coincided with sales drops or lifts.

---

## File

`dynamic_pricing_changes_{snapshot_date}.csv`

Drop the latest export here, dated to the day it was pulled. Re-pull weekly
through the run; we'll diff snapshots to reconstruct the price-change
timeline if the file ever gets purged of old changes.

**Grain:** one row per (show × price level × performance × enact-datetime).
Multiple rows per (show × price level × performance) — one for each price
change.

---

## Schema (confirmed)

| Field | Notes |
|---|---|
| `Show` | Production name (e.g., `& Juliet`, `Mamma Mia!`) — filter to Mamma Mia! and the comparable productions |
| `Price Level` | Zone + tier (e.g., `Balcony Level C`, `Mezzanine Level A`). Maps to the `zone_description` in the Performance Sales Analysis pull |
| `Enact Date` | Datetime the price became active (e.g., `5/1/2025 9:00`) |
| `Price` | New price as a string with `$` (e.g., `$75.00`) — strip the `$` and cast to numeric |
| `Event Date` | Performance date the price applies to (e.g., `8/13/2025 19:30`) |
| `Next Enactment Date` | When this price was superseded. **Empty = currently active.** |

**Constructed fields we'll derive in code:**

- `price_window_start = Enact Date`
- `price_window_end = Next Enactment Date` (or run end if NULL)
- For each (Show, Price Level, Event Date) we expect a **chain** of rows
  with no time gaps; `Next Enactment Date` of row N should equal
  `Enact Date` of row N+1.

---

## Filtering

The full file covers every show CTG runs. For this analysis we need:

- All rows where `Show = "Mamma Mia!"` (exact spelling — verify on receipt)
- All rows for the **comparable productions** identified in the README
  (so we can compare pricing-curve aggressiveness vs. their sold-through
  rates)

Keep the raw file unfiltered in this folder; we'll filter in code.

---

## Anomalies / notes

> Watch for these and log here:
> - Multiple rows with the same `Enact Date` for one (Show, Price Level,
>   Event Date) → duplicate / overwrite?
> - Gaps in the chain (row N's `Next Enactment Date` ≠ row N+1's `Enact Date`)
> - Price-level names that don't match the zones in the Performance Sales
>   Analysis pull (we'll need a mapping table)
> - Performances with no rows at all (= price never changed, or = missing data?)

-
-
