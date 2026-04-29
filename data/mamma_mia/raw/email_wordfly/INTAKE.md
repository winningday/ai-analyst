# Email — Wordfly Intake Checklist

Source: **Wordfly** (email platform), exported to CSV via the **Looker Studio**
report that merges Wordfly + Google Analytics attribution.

12 weeks of history. Filter to campaigns mentioning Mamma Mia! (or all
campaigns and we'll filter — easier if campaign naming is consistent).

---

## File

`wordfly_email_{start}_to_{end}.csv`

**Grain:** one row per campaign send (or per send × audience segment if the
report breaks it out).

**Required columns:**

| Field | Notes |
|---|---|
| `send_date` | When the email went out |
| `campaign_name` | Subject or internal name — must be filterable to Mamma Mia! |
| `audience_segment` | Subscribers, single-ticket buyers, lapsed, etc. |
| `sent` | Total recipients |
| `delivered` | After bounces |
| `opens` | Total opens |
| `unique_opens` | Distinct openers |
| `clicks` | Total clicks |
| `unique_clicks` | Distinct clickers |
| `unsubscribes` | |
| `bounces` | |
| `attributed_sessions` | From the GA merge in Looker Studio |
| `attributed_revenue` | From the GA merge — note this is GA-attributed, not Tessitura |

---

## Especially important for this analysis

- The **Monday email blast** during the drop week — capture send time, audience
  size, subject line, segment. That email is the leading hypothesis for
  pulling demand forward.
- Any **follow-up sends** later in the week (Wed/Thu/Fri reminders)? If none
  were planned, that's a finding.
- Send cadence in the 11 prior weeks — were there typically multiple sends
  per week? Did this week deviate?

---

## Anomalies / notes

-
-
