# Google Analytics — Intake Checklist

Source: **GA4** (CSV exports from the GA UI, since BigQuery isn't enabled).

Filter every report to the Mamma Mia! show pages. Use a page filter like
`pagePath contains "mamma-mia"` (adjust to actual URL slug).

12 weeks of history.

---

## 1. Daily acquisition

**File:** `ga_acquisition_{start}_to_{end}.csv`

Report: **Acquisition → Traffic acquisition** (or User acquisition).
Date range: last 12 weeks. Add a secondary dimension of `date`.

**Columns:**

| Field | Notes |
|---|---|
| `date` | Daily grain |
| `source` | google, facebook, direct, etc. |
| `medium` | cpc, organic, email, referral, etc. |
| `campaign` | Campaign name where present |
| `sessions` | |
| `new_users` | |
| `engaged_sessions` | GA4 engagement metric |
| `avg_session_duration` | Optional |

---

## 2. Daily ecommerce funnel

**File:** `ga_funnel_{start}_to_{end}.csv`

Report: **Monetization → Ecommerce purchases** (and Engagement → Events for
funnel events). If ecommerce tracking is configured for ticket purchases,
pull this. If not, skip and we'll use Tessitura.

**Columns:**

| Field | Notes |
|---|---|
| `date` | |
| `source_medium` | |
| `sessions` | |
| `view_item` (PDP views) | Show page views |
| `add_to_cart` | |
| `begin_checkout` | |
| `purchase` | |
| `purchase_revenue` | GA-attributed revenue (will not match Tessitura — that's expected) |

---

## 3. Landing pages

**File:** `ga_landing_pages_{start}_to_{end}.csv`

Report: **Engagement → Landing page**, filtered to Mamma Mia! pages.

**Columns:**

| Field | Notes |
|---|---|
| `date` | |
| `landing_page` | Path |
| `sessions` | |
| `bounce_rate` | |
| `conversions` | |

Used to spot a site issue (e.g., a landing page broke Friday).

---

## Anomalies / notes

-
-
