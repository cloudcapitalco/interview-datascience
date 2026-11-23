# Primer: commitments and who carries the gap

## What a commitment is

Cloud providers (AWS, Google Cloud, Azure) sell their services at a list price,
called on demand. They also sell a discount in exchange for a promise: the buyer
commits to a fixed amount of spend per hour on a group of services for one or three
years. In this challenge the discount is 28% and the term is one year.

The promise is paid in full whether it is used or not.

- **Usage above the commitment** is billed at the on-demand price. Nothing is lost
  except the discount that a larger commitment would have earned.
- **Usage below the commitment** leaves part of the commitment unused. That part is
  still paid.
- **The commitment is measured hour by hour.** An hour with low usage cannot borrow
  from an hour with high usage. Unused commitment in one hour is gone.

Each kind of commitment covers a particular group of services. The commitment in
this challenge is a Compute Savings Plan, which covers the `compute` service group
only. Databases and caches have their own kinds of commitment; they are not part of
this decision. Storage, network and most other services cannot be committed at
all.

## Who carries the gap

When a company buys its own commitment, the company carries the gap: if its usage
falls, it pays for capacity it no longer uses, for the rest of the term.

Cloud Capital makes the commitment to the provider itself. The customer pays Cloud
Capital for the usage it actually has, at a price below on demand. When the
customer's usage falls below the commitment, Cloud Capital pays the difference.
When the customer stops paying, Cloud Capital still owes the provider for the rest
of the term.

<!-- TODO(Brian): confirm this description of the products is the one we want
candidates to work from, and how much of the contract terms to show. -->

So Cloud Capital's exposure on an account has two parts:

1. **Usage risk.** The customer's compute usage falls below the commitment.
2. **Counterparty risk.** The customer cannot or will not pay.

## A few accounts dominate the book

The commitment book is concentrated. A handful of large customers make up most of
the committed dollars, so one large account going wrong costs more than many small
ones. `accounts.parquet` gives each account's share of the whole book if every
proposed commitment is approved.

## Words used in the data

| Term | Meaning here |
|---|---|
| On-demand cost | What the usage costs at list price. All costs in the data are at list price. |
| Compute usage | The usage this commitment can cover: the `compute` service group. |
| Covered cost | The part of a service's cost that the customer's existing commitments already cover. |
| Commitment level | Dollars per hour of compute usage, at list price, that the commitment covers. A level of $1,000 per hour costs $720 per hour at the 28% discount, every hour of the year. |
| Unused commitment | Commitment level minus compute usage, in each hour where usage is lower. |
