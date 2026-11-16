# TRACE-MoE: Open-Set Detection of Unknown Attacks in the Internet of Medical Things Using a Mixture-of-Experts Model and Energy Scores

This repository is the companion code and results for the paper of the same title, submitted to IEEE Open Journal of the Communications Society (OJ-COMS). It contains the full training and evaluation pipeline, all per-run result metrics, and the aggregation scripts that reproduce every table and claim in the paper.

TRACE-MoE is evaluated under a **leave-one-attack-out (LOAO)** open-set protocol on the CICIoMT2024 dataset (Wi-Fi and MQTT traffic). In each run, one attack class is withheld from training and treated as unknown at test time. Five seeds (42, 43, 44, 45, 46) are used for each of 3 models x 5 attack classes, giving **75 canonical runs** in total. The study tests five pre-registered hypotheses (H1-H5) covering energy-based unknown-attack detection, AUROC comparison, architecture ranking, closed-set degradation, and per-class ranking preservation.

---

## Training Settings

| Setting | Value |
|---|---|
| Seeds | 42, 43, 44, 45, 46 |
| Epochs | 50 (early-stopped; patience 10 on validation macro-F1) |
| Batch size | 256 |
| Learning rate | 0.001 (Adam, weight decay 1e-4) |
| Window length T | 16 flows |
| **TRACE-MoE** | d_model=128, n_heads=4, n_layers=2, ff_dim=256, n_experts=4, expert_hidden x 2 = 256 |
| **Transformer** | d_model=128, n_heads=4, n_layers=2, ff_dim=256 |
| **BiLSTM-DNN** | d_model=128, T=1 (row-level) |
| Abstain threshold | target_coverage=0.95 (95% of known validation windows accepted) |

---

## Repository Structure

```
TRACE-MoE-OpenSet-CICIoMT2024-release/
├── README.md
├── LICENSE
├── NOTICE
├── CITATION.cff
├── .gitignore
├── TRACEABILITY.md
├── data_access.md
├── requirements.txt
├── paper_ojcoms.pdf
├── SHASUMS
├── scripts/
│   ├── 07_unknown_attacks.py
│   ├── _common.py
│   ├── paper4_h8_verdict.py
│   ├── paper4_build_table.py
│   └── 25_twin_verdict_paper4.py
├── src/
│   └── trace_iomt/
│       ├── __init__.py
│       ├── abstain.py
│       ├── attacks.py
│       ├── audit.py
│       ├── compare.py
│       ├── config.py
│       ├── efficiency.py
│       ├── experiment.py
│       ├── metrics.py
│       ├── reporting.py
│       ├── result_doc.py
│       ├── train.py
│       ├── utils.py
│       ├── data/
│       │   ├── __init__.py
│       │   ├── labels.py
│       │   ├── loaders.py
│       │   ├── preprocess.py
│       │   └── windows.py
│       ├── datasets/
│       │   ├── __init__.py
│       │   ├── labels.py
│       │   ├── loaders.py
│       │   ├── preprocess.py
│       │   └── schema.py
│       └── models/
│           ├── __init__.py
│           ├── classical.py
│           ├── factory.py
│           ├── heads.py
│           └── networks.py
└── results/
    ├── H1_safety_view.csv
    ├── H1_safety_view.md
    ├── H2_energy_vs_msp.csv
    ├── H2_energy_vs_msp.md
    ├── H3_trace_moe_vs_baselines.csv
    ├── H3_trace_moe_vs_baselines.md
    ├── H4_closed_set_degradation.csv
    ├── H4_closed_set_degradation.md
    ├── ESA1_calibration.csv
    ├── ESA1_calibration.md
    ├── ESA2_DEFERRED.md
    ├── paper4_table_main.md
    ├── per_seed_tables.csv
    ├── twin_h5_verdict.csv
    ├── twin_h5_verdict.md
    ├── twin_h5_verdict.json
    ├── verdict.json
    ├── VERDICT_READING_NOTE.md
    ├── VERDICT_SUMMARY_v1_3_5seed.md
    └── per_run/
        └── <model>_loao_T16_<attack>_seed<s>/
            ├── metrics.json
            └── twin_h5_score.json
```

---

## Steps to Reproduce

**Step 1 (heavy, ~GPU hours):** Run all 75 LOAO training and evaluation runs:

```bash
python scripts/07_unknown_attacks.py --config configs/paper3_openset.yaml
```

This trains and evaluates 3 models x 5 attack classes x 5 seeds = 75 runs and writes per-run outputs to `results_v3_paper3/zero_day/`. Note: this step requires the raw CICIoMT2024 CSVs (see `data_access.md`) and a `configs/` directory (not included in this release; see note below).

**Step 2 (seconds):** Aggregate H1-H4 and ESA1 from per-run metrics:

```bash
python scripts/paper4_h8_verdict.py
```

Reads `results/per_run/*/metrics.json` and writes `results/H1_safety_view.csv`, `H2_energy_vs_msp.csv`, `H3_trace_moe_vs_baselines.csv`, `H4_closed_set_degradation.csv`, `ESA1_calibration.csv`.

**Step 3 (seconds):** Aggregate H5 (PCRP) from per-run twin scores:

```bash
python scripts/25_twin_verdict_paper4.py
```

Reads `results/per_run/*/twin_h5_score.json` and writes `results/twin_h5_verdict.csv`.

**Step 4 (seconds):** Render the main results table:

```bash
python scripts/paper4_build_table.py
```

Writes `results/paper4_table_main.md`.

> **Note on Steps 2-4:** These scripts can be run against the per-run data already in `results/per_run/` without re-running Step 1. The aggregated results in `results/` were produced from exactly these per-run files.
>
> **Note on configs/:** Step 1 additionally requires the `configs/` directory, which is not included in this release. The `configs/` directory contains only experiment-setup files (paths, logging, run-management settings), not scientific parameters. All scientific settings are fully documented in the Training Settings table above and in the paper.

---

## Quick Verification

To verify a specific number, for example TRACE-MoE's mean safety-view detection rate for ARP Spoofing:

1. Open `results/H1_safety_view.csv`
2. Find the row for `ARP_Spoofing` (should be 0.9762 mean)
3. Cross-check against `results/per_run/trace_moe_loao_T16_ARP_Spoofing_seed42/metrics.json` (key: `safety_view_auroc` or `ood_auroc`)
4. Compare to Table 1 in `paper_ojcoms.pdf`

The TRACEABILITY.md file maps every table row and abstract number to its source file.

---

## Checksum Verification

SHASUMS lists the SHA-256 checksum of every file in this release.

To verify all checksums:

```bash
# Linux / macOS
sha256sum --check SHASUMS

# Windows (PowerShell, one file at a time)
certutil -hashfile paper_ojcoms.pdf SHA256
```

---

## What IS Included

- Paper PDF (`paper_ojcoms.pdf`)
- LOAO training and evaluation script (`scripts/07_unknown_attacks.py`) and shared CLI utilities (`scripts/_common.py`)
- Aggregation scripts (`scripts/paper4_h8_verdict.py`, `scripts/25_twin_verdict_paper4.py`, `scripts/paper4_build_table.py`)
- Model definitions, data-loading, and training source code (`src/trace_iomt/`)
- Aggregated hypothesis result tables H1-H5 and ESA1 (`results/*.csv` and `results/*.md`)
- Per-run metrics for all 75 canonical runs (`results/per_run/*/metrics.json` and `twin_h5_score.json`)
- Standard files (LICENSE, NOTICE, CITATION.cff, TRACEABILITY.md, data_access.md, requirements.txt, SHASUMS)

## What is NOT Included

- Raw CICIoMT2024 dataset CSVs (obtain from https://www.unb.ca/cic/datasets/iomt-dataset-2024.html -- see `data_access.md`)
- Configuration files (`configs/` directory; scientific settings are fully documented above and in the paper)
- Model checkpoints (`model.pt`, 75 files; reproducible by re-running Step 1)
- Per-run predictions (`predictions.npz`)
- Per-run training history (`history.csv`)
- Figure generation scripts
- Manuscript source files

---

## Citation

If you use this code or these results, please cite:

```
Sudhir Kumar Sharma and Sneha Vasishth, "TRACE-MoE: Open-Set Detection of Unknown
Attacks in the Internet of Medical Things Using a Mixture-of-Experts Model and
Energy Scores," IEEE Open Journal of the Communications Society, 2026.
```

See `CITATION.cff` for a machine-readable citation.

---

## License

Apache License 2.0. See `LICENSE` and `NOTICE` for details.
The CICIoMT2024 dataset is subject to its own terms; see `data_access.md`.
