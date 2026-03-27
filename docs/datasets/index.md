# Dataset Registry

All datasets in this hub are **pointer-only** — we do not commit large raw data files. Each entry links to the source, describes the license, and includes an EA-DX dataset card.

## Policy

- Datasets must have a clear open license (CC0, CC BY, ODC-By, ODbL, or similar)
- No customer PII, no CEII — synthetic or fully anonymised data only
- Every dataset must have a [dataset card](template.md) in `docs/datasets/`

## Featured: GridFM DataKit

!!! tip "Foundation model training data"
    The [LF Energy GridFM project](https://lfenergy.org/projects/gridfm/) provides [`gridfm-datakit`](https://github.com/gridfm/gridfm-datakit) — a Python library for generating **synthetic, realistic power flow (PF) and optimal power flow (OPF) datasets** from MATPOWER/PGLib reference networks.

    Unlike static datasets, it generates data on demand at scale (up to 30,000 buses). Ideal for pre-training foundation models or benchmarking ML-OPF solvers.

    [:octicons-arrow-right-24: GridFM DataKit dataset card](gridfm-datakit.md)

## Curated datasets

| Dataset | Domain | Task | License | Size | Card |
|---------|--------|------|---------|------|------|
| [GridFM DataKit](https://github.com/gridfm/gridfm-datakit) ⭐ | Transmission | Optimization, EDA | Apache-2.0 | On-demand | [Card](gridfm-datakit.md) |
| [Open Power System Data](https://open-power-system-data.org/) | Generation / Transmission | Forecasting, EDA | CC BY 4.0 | ~GB | — |
| [ERCOT hourly load](https://www.ercot.com/gridinfo/load/load_hist) | Markets | Forecasting | Public | MB | — |
| [GEFCom 2014](https://www.kaggle.com/datasets/robikscube/gefcom2014) | Generation / Markets | Forecasting | Varies | MB | — |
| [NREL NSRDB](https://nsrdb.nrel.gov/) | Generation (solar) | DER forecasting | CC BY 4.0 | Large | — |
| [PecanStreet Dataport](https://www.pecanstreet.org/dataport/) | Customer / DER | Forecasting, anomaly | Varies (registration) | GB+ | — |
| [UCI Individual Household Power](https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption) | Customer | EDA, anomaly | CC BY 4.0 | 132 MB | — |

!!! warning "Verify license before use"
    Dataset availability and license terms change. Always check the source before training or publishing models.

## Adding a dataset

1. Write a [dataset card](template.md) in `datasets/cards/<name>.md`
2. Add a download script or instructions in `datasets/index/`
3. Open a PR — the sensitive data checklist applies

See [CONTRIBUTING.md](../contributing.md) for the full process.
