# Commitment Risk Challenge

Cloud Capital is about to make a one-year promise to a cloud provider on behalf of
each of five customer accounts. You get their daily cloud usage, a one-page primer
on how these promises work, and up to three hours. Tell us what could go wrong.

Start with the [primer](docs/primer.md), then the [challenge](docs/challenge.md).

## Who you are writing for

Your memo goes to an executive who will decide whether to make these promises. They
are not a data scientist and will not read your notebook. Write so they can act on
what you say: what the risk is, how large it could be, what we do not know yet, and
how we would find out. Plan to spend a good share of your time on the memo.

## Quickstart

This project uses [`uv`](https://docs.astral.sh/uv/). From the repo root:

```sh
# 1. Install uv (skip if you already have it)
curl -LsSf https://astral.sh/uv/install.sh | sh

# 2. Build an isolated environment with all dependencies
uv sync

# 3. Launch Jupyter and open the starter notebook
uv run jupyter lab notebooks/starter.ipynb
```

`uv sync` creates a `.venv` with DuckDB, pandas, matplotlib and JupyterLab;
`uv run …` runs a command inside it.

> **Setting up with an agent?** Paste the three commands above and ask it to get
> JupyterLab running and confirm `notebooks/starter.ipynb` runs top to bottom.

## The data

The data ships with this repository in `data/`. It is daily cloud usage for five
anonymized accounts. Account names, dates and dollar amounts have been changed.

<!-- TODO(Brian): the prototype ships synthetic stand-ins. Replace with anonymized
real data before any candidate sees it. -->

## Where to go

| | |
|---|---|
| [docs/primer.md](docs/primer.md) | What a commitment is and who pays when usage falls. One page. |
| [docs/challenge.md](docs/challenge.md) | The question, the limits, and what to send back. |
| [docs/data_dictionary.md](docs/data_dictionary.md) | Every column in `data/`. |
| [docs/understanding_debt.md](docs/understanding_debt.md) | What we value. Read this before you start. |
| [docs/understanding_ledger.md](docs/understanding_ledger.md) | The short ledger to submit with your work. |
| [notebooks/starter.ipynb](notebooks/starter.ipynb) | Loads the data. Nothing else. |
