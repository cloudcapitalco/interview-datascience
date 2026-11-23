# Data dictionary

Two Parquet files, provided separately and placed in `data/`. The data is
**anonymized real data** from five Cloud Capital customers. Account names are
replaced by letters, every timestamp is shifted by the same number of whole weeks,
and each account's dollar amounts are multiplied by its own factor. Hours of the
day, weekdays, the shape of usage over time, and the order of events across
accounts are kept. Holidays fall on the wrong calendar dates.

## `data/hourly_usage.parquet`

**Grain:** one row per account, per hour, per service group. An hour with no usage
in a service group has no row.

| Column | Type | Definition |
|---|---|---|
| `timestamp` | timestamp | Start of the hour (UTC), shifted. |
| `account` | string | Account code, `A` to `E`. |
| `service` | string | Service group: `compute`, `database`, `cache`, `storage`, `network`, `other`. The proposed commitment covers `compute` only. |
| `on_demand_cost` | double | Cost of the hour's usage at list price, with no discount, in US dollars. |
| `covered_cost` | double | The part of `on_demand_cost` that the customer's existing commitments covered, at list price. Zero where no commitment applied. |

Some services post charges once a day or once a month instead of every hour, so
their hourly series can look lumpy. Compute is metered hourly.

Each account's history ends at 23:00 on its own `decision_date` (see below).
Accounts start on different dates.

## `data/accounts.parquet`

**Grain:** one row per account.

| Column | Type | Definition |
|---|---|---|
| `account` | string | Account code, matches `hourly_usage.parquet`. |
| `history_start` | date | First day of data for the account. |
| `decision_date` | date | Last day of data. The proposed commitment starts at midnight after it. |
| `proposed_compute_commitment_usd_per_hour` | double | The one-year compute commitment under consideration, as dollars per hour of compute usage at list price. It replaces the existing compute commitments from its start. |
| `proposed_term_months` | int | Length of the proposed term. |
| `share_of_book_pct` | double | This account's share of Cloud Capital's whole commitment book, all customers included, if every proposal is approved. |
