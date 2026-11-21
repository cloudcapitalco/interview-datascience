# Data dictionary

Two Parquet files, provided separately and placed in `data/`. The data is
**anonymized real data** from five Cloud Capital customers. Account names are
replaced by letters, every date is shifted by the same number of whole weeks, and
each account's dollar amounts are multiplied by its own factor. Weekdays, the shape
of usage over time, and the order of events across accounts are kept. Holidays fall
on the wrong calendar dates.

## `data/daily_usage.parquet`

**Grain:** one row per account, per day, per service group.

| Column | Type | Definition |
|---|---|---|
| `date` | date | Calendar day (UTC), shifted. |
| `account` | string | Account code, `A` to `E`. |
| `service` | string | Service group: `compute`, `database`, `cache`, `storage`, `network`, `other`. |
| `eligible` | boolean | True when a commitment can cover this usage. True for `compute`, `database` and `cache`. |
| `on_demand_cost` | double | Cost of the day's usage at list price, with no discount, in US dollars. |
| `covered_cost` | double | The part of `on_demand_cost` that the customer's existing commitments covered, at list price. Zero where no commitment applied. |

Each account's history ends on its own `decision_date` (see below). Accounts start
on different dates.

## `data/accounts.parquet`

**Grain:** one row per account.

| Column | Type | Definition |
|---|---|---|
| `account` | string | Account code, matches `daily_usage.parquet`. |
| `history_start` | date | First day of data for the account. |
| `decision_date` | date | Last day of data. The proposed commitment starts the next day. |
| `proposed_commitment_usd_per_day` | double | The one-year commitment under consideration, as dollars per day of eligible usage at list price. It replaces the existing commitments from its start. |
| `proposed_term_months` | int | Length of the proposed term. |
| `share_of_book_pct` | double | This account's share of Cloud Capital's whole commitment book, all customers included, if every proposal is approved. |

Commitment levels are given per day for convenience. The commitment itself applies
hour by hour; see the [primer](./primer.md).
