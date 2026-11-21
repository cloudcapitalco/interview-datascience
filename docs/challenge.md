# The challenge

Cloud Capital is about to make a one-year commitment against each of the five
accounts in the data. Each account has its own decision date in `accounts.parquet`:
its usage history ends that day and the proposed commitment starts the next. The
proposed levels are in the same file.

Read the [primer](./primer.md) first.

## The questions

For each account, and for the five together:

1. **What could go wrong?** Name the ways this promise could cost us money.
2. **How large?** Give an order of magnitude in dollars, and say what it depends on.
3. **What would you want to know that is not here?** Data, documents, conversations.
4. **How would you find out?** For each thing you want to know, how you would get it
   and how you would check it.
5. **What from your own field does this resemble, and where does the resemblance
   break?** Use what you already know about financial risk. Tell us where the
   analogy holds and where it stops holding.

We want to see how you look at the data and reason about risk. We are not asking
you to build a forecasting or pricing model. If you fit something to the data, tell
us how you checked it.

## Limits

- **Three hours at most.** Stop when you reach them, and tell us where you stopped.
- **No model build.** Exploration, description and reasoning.
- **AI tools are allowed.** Say how you used them in your
  [understanding ledger](./understanding_ledger.md).

<!-- TODO(Brian): paid or unpaid. -->

## What to send back

Package your work as a git repository or a zip and send it to the person who sent
you this challenge.

- **A memo of at most two pages** for the executive who decides on these
  commitments. Plain language, no code. Figures are welcome if they carry a point.
- **Your notebook**, runnable from the two data files in `data/`.
- **An [understanding ledger](./understanding_ledger.md).** Read
  [what we value](./understanding_debt.md) first.

## What happens next

A 75-minute working session with three of us. You present your memo, we discuss it,
and we work through a related problem together. Nothing to prepare beyond the memo.
