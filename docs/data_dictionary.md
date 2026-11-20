# Data dictionary

Two CSV files in `data/`. Account names, dates and dollar amounts have been changed
so that no customer can be identified. Within an account, the shape of usage over
time is kept.

## `data/daily_usage.csv`

**Grain:** one row per account, per day, per service.

| Column | Type | Definition |
|---|---|---|
| `date` | date | Calendar day (UTC). |
| `account` | string | Account code, `A` to `E`. |
| `service` | string | Service group: `compute`, `gpu_compute`, `database`, `cache`, `storage`, `network`, `other`. The first four are eligible for commitment coverage. |
| `cost_usd` | float | On-demand cost of the day's usage in US dollars: what it would cost at list price with no discount. |

Accounts have different start dates. Every history ends on 2025-09-30.

## `data/accounts.csv`

**Grain:** one row per account.

| Column | Type | Definition |
|---|---|---|
| `account` | string | Account code, matches `daily_usage.csv`. |
| `history_start` | date | First day of data for the account. |
| `existing_commitment_usd_per_day` | float | Commitment already in place, as on-demand-equivalent eligible usage per day. 0 if none. |
| `existing_commitment_ends` | date | Last day of the existing commitment. Empty if none. |
| `proposed_commitment_usd_per_day` | float | The new one-year commitment under consideration, in the same units. It replaces any existing commitment from its start date. |
| `proposed_term_start` | date | Start of the proposed term. |
| `proposed_term_months` | int | Length of the proposed term. |
| `share_of_book_pct` | float | This account's share of Cloud Capital's whole commitment book, all customers included, if every proposal is approved. |

Commitment levels are given per day for convenience. The commitment itself applies
hour by hour; see the [primer](./primer.md).
