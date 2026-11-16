# Traceability: Paper Numbers to Source Files

This document maps every reported number, table, and figure in the paper to its source file(s) in this release and the aggregation script that produced it.

Paper table numbering: Table 1 = H1 (safety-view), Table 2 = H3 (architecture comparison), Table 3 = H2 (energy vs MSP), Table 4 = H4 (closed-set degradation), Table 5 = H5 (PCRP AUROC), Table 6 = ESA1 (calibration).

Figure numbering: Fig. 1 = architecture diagram, Fig. 2 = H1 bar chart, Fig. 3 = H3 bar chart, Fig. 4 = H2 bar chart, Fig. 5 = H4 bar chart, Fig. 6 = H5 PCRP bar chart.

| Paper item | Source file(s) in this release | Produced by |
|---|---|---|
| Abstract: H1 mean safety-view detection rates 0.9762 to 1.0000 | `results/H1_safety_view.csv` (column: mean) | `scripts/paper4_h8_verdict.py` |
| Abstract: H2 overall verdict "not supported" | `results/H2_energy_vs_msp.csv` (column: verdict) | `scripts/paper4_h8_verdict.py` |
| Abstract: H3 TRACE-MoE vs BiLSTM-DNN, 4 of 5 classes, mean advantages 0.1553 to 0.3182 | `results/H3_trace_moe_vs_baselines.csv` (column: mean_diff, verdict) | `scripts/paper4_h8_verdict.py` |
| Abstract: H4 max degradation 2.47 pp for TRACE-MoE | `results/H4_closed_set_degradation.csv` (column: mean_drop_pp) | `scripts/paper4_h8_verdict.py` |
| Abstract: H5 4 of 5 classes supported | `results/twin_h5_verdict.csv` (column: verdict) | `scripts/25_twin_verdict_paper4.py` |
| Table 1 (H1 safety view) -- all 5 rows, all columns (seed42-seed46, mean, ci_lo, ci_hi, verdict) | `results/H1_safety_view.csv` | `scripts/paper4_h8_verdict.py` |
| Table 2 (H3 architecture comparison) -- all rows (transformer and bilstm_dnn vs TRACE-MoE, per class) | `results/H3_trace_moe_vs_baselines.csv` | `scripts/paper4_h8_verdict.py` |
| Table 3 (H2 energy vs MSP AUROC) -- all rows (per class, per model) | `results/H2_energy_vs_msp.csv` | `scripts/paper4_h8_verdict.py` |
| Table 4 (H4 closed-set degradation) -- all rows (TRACE-MoE, Transformer, BiLSTM-DNN per class) | `results/H4_closed_set_degradation.csv` | `scripts/paper4_h8_verdict.py` |
| Table 5 (H5 PCRP AUROC) -- all rows (per class, per seed, mean, CI, verdict) | `results/twin_h5_verdict.csv` | `scripts/25_twin_verdict_paper4.py` |
| Table 6 (ESA1 calibration) -- all rows (ECE, MCE per model) | `results/ESA1_calibration.csv` | `scripts/paper4_h8_verdict.py` |
| Fig. 2 (H1 safety-view bar chart data) | `results/H1_safety_view.csv` | `scripts/paper4_h8_verdict.py` |
| Fig. 3 (H3 architecture comparison bar chart data) | `results/H3_trace_moe_vs_baselines.csv` | `scripts/paper4_h8_verdict.py` |
| Fig. 4 (H2 energy vs MSP bar chart data) | `results/H2_energy_vs_msp.csv` | `scripts/paper4_h8_verdict.py` |
| Fig. 5 (H4 closed-set degradation bar chart data) | `results/H4_closed_set_degradation.csv` | `scripts/paper4_h8_verdict.py` |
| Fig. 6 (H5 PCRP bar chart data) | `results/twin_h5_verdict.csv` | `scripts/25_twin_verdict_paper4.py` |
| Section VI main claim: "TRACE-MoE's safety-view detection rate is supported (strong) on all five held-out classes" | `results/H1_safety_view.csv` (all verdict cells = "SUPPORTED (strong)") | `scripts/paper4_h8_verdict.py` |
| Section VI degradation ratios: BiLSTM-DNN degradation 3.3 to 4.8x larger than TRACE-MoE's | `results/H4_closed_set_degradation.csv` (columns: mean_drop_pp per model, ratios derived from these values) | `scripts/paper4_h8_verdict.py` |
| Section VI MQTT-DDoS claim: mean advantage 0.1658, CI -0.0147 to +0.3700 | `results/H3_trace_moe_vs_baselines.csv` (baseline=bilstm_dnn, class=MQTT-DDoS-Publish_Flood) | `scripts/paper4_h8_verdict.py` |
| Overall hypothesis verdicts summary | `results/verdict.json` | `scripts/paper4_h8_verdict.py` |
| Per-seed detail for all hypotheses | `results/per_seed_tables.csv` | `scripts/paper4_h8_verdict.py` |

---

All per-run raw data is in `results/per_run/`. Each subdirectory corresponds to one of the 75 canonical LOAO runs and contains:
- `metrics.json`: all closed-set and open-set metrics for that run (closed-set macro-F1, per-class F1, energy-based AUROC per class, MSP-based AUROC per class, abstain metrics, calibration metrics)
- `twin_h5_score.json`: the per-class PCRP score used for H5 aggregation

The aggregation scripts (`paper4_h8_verdict.py` and `25_twin_verdict_paper4.py`) reproduce every row of every hypothesis CSV from these per-run files. Running Steps 2-3 from the README reproduces all table values.
