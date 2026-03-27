# Advanced

**Level:** Research / Expert  
**Prerequisites:** Strong ML background; familiarity with energy market structures  
**Notebooks:** `notebooks/advanced/`

---

## Curriculum overview

### Foundation models for power grids

Large AI models pre-trained on broad grid datasets and fine-tuned for specific downstream tasks. The [LF Energy GridFM project](https://lfenergy.org/projects/gridfm/) is the leading open initiative here — backed by Hydro-Québec and IBM.

Key concepts:
- **Masked power flow pre-training** — analogous to BERT's masked language modeling, but for grid state variables (voltage magnitudes, angles, power injections)
- **Surrogate solvers** — FM replaces or accelerates slow numerical OPF solvers
- **Fine-tuning on proprietary data** — utilities adapt a shared pre-trained model without sharing raw data

See the [Foundation Models for Grids](../concepts/foundation-models.md) concept page for a full overview, including how to generate training data with [gridfm-datakit](../datasets/gridfm-datakit.md).

### Grid optimization and RL

The grid is a sequential decision problem. Reinforcement learning agents can learn dispatch schedules, topology switching actions, and storage arbitrage strategies.

- [Grid2Op](https://github.com/rte-france/Grid2Op) — leading RL framework for power grid environments
- [Pandapower](https://pandapower.readthedocs.io/) — power flow simulation
- [GridFM-compatible environments](https://github.com/gridfm/gridfm-datakit) — synthetic datasets from gridfm-datakit work as RL environment seeds
- Safe exploration: hard constraints (thermal limits, voltage limits) must always be satisfied

### Federated learning for energy

Utilities can't always share raw customer or operational data. Federated learning trains models across distributed data owners without centralizing data.

Key references:
- FedAvg in heterogeneous energy contexts
- Privacy-preserving load disaggregation
- Cross-utility load forecasting

### Benchmarking and reproducibility

Research reproducibility in energy ML is poor. Best practices:

- Fixed random seeds and temporal splits
- Versioned datasets with EA-DX packages
- Standardized metrics reported on held-out test sets
- Model cards and result tables with uncertainty estimates

### Model governance

- **Model cards** (Mitchell et al., 2019) — intended use, performance across subgroups, ethical considerations
- **Datasheets for datasets** (Gebru et al., 2021) — motivation, composition, collection, preprocessing
- **NIST AI RMF** — four functions: Govern, Map, Measure, Manage
- **EU AI Act** — energy grid management systems may be classified as high-risk (Annex III)

---

## Notebooks (planned)

| Notebook | Domain | Status |
|----------|--------|--------|
| `01_foundation_model_intro.ipynb` | Transmission | 📋 Planned — GridFM DataKit + masked PF pre-training setup |
| `02_gridfm_datakit_walkthrough.ipynb` | Transmission | 📋 Planned — generate PF/OPF data, export to EA-DX |
| `03_grid2op_intro.ipynb` | Transmission / Distribution | 📋 Planned |
| `04_storage_arbitrage_rl.ipynb` | Markets / DER | 📋 Planned |
| `05_federated_load_forecasting.ipynb` | Customer | 📋 Planned |
| `06_model_card_template.ipynb` | Governance | 📋 Planned |
| `07_benchmarking_best_practices.ipynb` | Cross-domain | 📋 Planned |
