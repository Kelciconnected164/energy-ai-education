# Foundation Models for Energy Grids

Foundation models (FMs) are large AI models pre-trained on broad datasets and fine-tuned for specific downstream tasks. Powerful FMs exist for language (GPT, Claude), vision (SAM), and weather (Pangu-Weather, GraphCast). The energy sector is now building its own.

---

## Why foundation models for the grid?

The electric power grid is one of the most complex engineered systems on Earth. It faces:

- **Increasing variability** from renewable DER (wind, solar, batteries, EVs)
- **Combinatorial complexity** — millions of operating states across thousands of assets
- **Data silos** — each utility has proprietary data and grid-specific requirements
- **Compute bottlenecks** — full AC power flow and optimal power flow (OPF) solvers can take minutes at scale

Foundation models pre-trained on large synthetic or federated grid datasets can:

- **Accelerate computation** — replace or complement slow numerical solvers
- **Enable fine-tuning** — utilities adapt a shared pre-trained model with their private data (economically)
- **Generalize across topologies** — one model, many grid configurations

---

## The GridFM initiative

**GridFM** is an open-source LF Energy Sandbox project building foundation models for power grids, led by Hydro-Québec and IBM.

> *"Foundation models for the electric power grid have the potential to cope with the increasing complexity and uncertainties stemming from the energy transition."*
> — [LF Energy GridFM project page](https://lfenergy.org/projects/gridfm/)

### What GridFM is doing

**Phase 1 — Data:** Establish a large collection of solved AC power flow cases across different grid topologies, parameters, and load conditions. This is where [gridfm-datakit](https://github.com/gridfm/gridfm-datakit) comes in — a Python library for generating scalable synthetic PF/OPF datasets.

**Phase 2 — Model (GridFM-v0):** Pre-train a model to reconstruct masked power flow data (similar to BERT's masked language modeling, but for grid state variables like voltage magnitudes and angles).

**Phase 3 — Fine-tuning:** Test and fine-tune on proprietary utility data for downstream applications:
- Complementing numerical power flow solvers
- Contingency analysis
- Optimal power flow (OPF)

### Why this matters for energy ML practitioners

| Without GridFM | With GridFM |
|---------------|------------|
| Train from scratch on small datasets | Fine-tune a pre-trained model with less data |
| Slow OPF solvers as ground truth | FM surrogate as fast approximate solver |
| Topology-specific models | Single model generalizes across grid configurations |
| Utility data stays siloed | Fine-tune privately; share the base model |

---

## gridfm-datakit — synthetic power flow generation

[`gridfm-datakit`](https://github.com/gridfm/gridfm-datakit) (Apache-2.0) generates realistic, diverse, scalable synthetic datasets for power flow (PF) and optimal power flow (OPF) ML problems.

**Key capabilities:**

- Scales to **30,000 buses** (PF) / **10,000 buses** (OPF)
- Compatible with **MATPOWER `.m` files** and the **PGLib dataset**
- Realistic load scenarios: combines global temporal profiles with per-bus spatial noise
- Flexible topology perturbations: handles N-k outages for lines, transformers, generators
- Generator cost diversity for OPF generalization
- Out-of-operating-limits scenarios (voltage violations, overloads)

```bash
pip install gridfm-datakit
```

### Relation to EA-DX

GridFM-generated power flow datasets map naturally to EA-DX:

| GridFM output | EA-DX representation |
|--------------|---------------------|
| Bus voltage magnitude | `measurement: voltage`, `entity_type: feeder` |
| Bus active power injection | `measurement: active_power`, `entity_type: feeder` |
| Line flow | `measurement: active_power`, `entity_type: feeder` |
| Load scenarios | `quality_flag: simulated`, `source: sim` |
| Topology state (line outage) | EA-DX `events.csv`, `event_type: switching` |

See the [EA-DX format](../eadx/index.md) for the full schema.

---

## Other relevant LF Energy projects

| Project | What it does | Relation |
|---------|-------------|----------|
| [GridFM](https://lfenergy.org/projects/gridfm/) | Foundation models for power grids | Primary reference |
| [PowerGridModel](https://github.com/PowerGridModel) | Fast power flow calculation engine (C++/Python) | Data generation backend |
| [PowSyBl](https://www.powsybl.org/) | Power system blocks (Java + Python) | Grid modelling |
| [DynaWo](https://dynawo.github.io/) | Dynamic power system simulation | Time-series generation |
| [OpenSynth](https://lfenergy.org/projects/opensynth/) | Synthetic energy data generation | Complementary to EA-DX |

---

## Learning path

For foundation model content in this hub, see:

- [Advanced track](../learning-paths/advanced.md) — GridFM-aligned notebooks (grid RL, benchmarking, reproducibility)
- [Datasets: gridfm-datakit card](../datasets/gridfm-datakit.md) — synthetic PF/OPF dataset generation
- [Benchmarks: Power flow surrogate](../benchmarks/index.md) — planned benchmark task using GridFM data

---

## Further reading

- [LF Energy GridFM project](https://lfenergy.org/projects/gridfm/)
- [gridfm/gridfm-datakit on GitHub](https://github.com/gridfm/gridfm-datakit)
- [LF Energy TAC proposal #260](https://github.com/lf-energy/tac/issues/260) — full technical proposal
- [LF Energy Grid Simulation & Modeling SIG](https://lfenergy.org/groups/grid-simulation-and-modeling-sig/)
- Donnot et al. (2017) — *"Introducing machine learning for power system operation support"*
- Zamzam & Baker (2020) — *"Learning Optimal Solutions for Extremely Fast AC Optimal Power Flow"*
