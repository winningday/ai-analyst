# Digital Advertising — Intake Checklist

Source: **External agency / digital advertising partner.** Request a CSV pull
from them.

12 weeks of history, daily grain, broken out by platform and campaign.

---

## File(s)

One file per platform is cleanest:

```
ads_meta_{start}_to_{end}.csv
ads_google_{start}_to_{end}.csv
ads_{other}_{start}_to_{end}.csv
```

Or a single combined file with a `platform` column — also fine.

**Grain:** one row per `date × platform × campaign × ad_set`.

**Required columns:**

| Field | Notes |
|---|---|
| `date` | Daily |
| `platform` | meta / google / tiktok / display / etc. |
| `campaign` | |
| `ad_set` | One level down from campaign |
| `objective` | Awareness / traffic / conversions |
| `impressions` | |
| `clicks` | |
| `spend` | In local currency |
| `frequency` | Avg impressions per user (Meta) |
| `reach` | Unique users (Meta) |
| `conversions` | Per the platform's pixel |
| `attributed_revenue` | If tracked |

---

## Critical questions to ask the agency

These often matter more than the metrics themselves. Get answers in writing
and drop them into the `## Anomalies / notes` section below.

1. **Were any campaigns paused, ended, or rotated mid-week?**
   (Hypothesis: ad pressure dropped Wed–Fri.)
2. **Did any campaigns hit daily / weekly budget caps?**
3. **Was there an audience refresh, or did the same audience get hit
   throughout the week?** (Frequency fatigue hypothesis.)
4. **Were creative variants rotated or did one fatigue?**
5. **Any platform-side issues** (account flagged, ad disapproval, tracking
   pixel firing issues)?
6. **Send a campaign change log** if available — paused/launched/edited
   timestamps.

---

## Anomalies / notes

-
-
