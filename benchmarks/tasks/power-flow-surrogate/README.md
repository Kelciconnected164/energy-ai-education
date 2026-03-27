# Benchmark: Power Flow Surrogate (GridFM data)

**Task ID:** `power-flow-surrogate`  
**Domain:** Transmission  
**EA-DX tasks:** optimization  
**Maturity:** Advanced  
**Status:** 📋 Planned  
**Related:** [LF Energy GridFM project](https://lfenergy.org/projects/gridfm/)

---

## Task definition

Given a set of bus active/reactive power injections and network topology, predict:

- Bus voltage magnitudes (`V`, p.u.)
- Bus voltage angles (`θ`, rad)
- Line active/reactive power flows

This is the **AC power flow approximation** task — replace or accelerate a numerical power flow solver with a trained ML surrogate.

## Dataset

Generated using [`gridfm-datakit`](https://github.com/gridfm/gridfm-datakit) on the `case118` MATPOWER reference network.

```bash
pip install gridfm-datakit
# See datasets/cards/gridfm-datakit.md for generation scripts
```

## Split protocol

| Split | Description |
|-------|-------------|
| **Train** | 80,000 operating snapshots (perturbed loads + topology) |
| **Validation** | 10,000 snapshots (held out during training) |
| **Test** | 10,000 snapshots (never seen during training/tuning) |

Snapshots are generated independently — no temporal ordering required.

## Metrics

| Metric | Variable | Unit | Direction |
|--------|---------|------|-----------|
| MAE | Voltage magnitude `V` | p.u. | lower is better |
| MAE | Active power flow `P` | MW | lower is better |
| MAE | Reactive power flow `Q` | MVAR | lower is better |
| Max error | `V` | p.u. | lower is better |
| Constraint violation rate | Thermal / voltage limits | % snapshots | lower is better |

## Baselines (planned)

| Baseline | Description |
|----------|-------------|
| `dc_approximation` | Linear DC power flow approximation |
| `mlp_baseline` | 3-layer MLP on node features |
| `gnn_baseline` | Graph neural network respecting grid topology |

## Changelog

| Version | Date | Change |
|---------|------|--------|
| 0.1.0 | 2026-03-27 | Initial stub |
