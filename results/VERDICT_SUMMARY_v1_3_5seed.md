# Paper 4 H1-H4 Verdict Summary — v1.3 (5-seed scope)

**Latest Charter SHA256 (v1.3)**: `130767067f36261dca0370a12c418da70bf081a249ce380f6df613508f675a42`
**Statistical recipe** (unchanged since v1.1): SHA256 `e1d29fc2b3278515579599bd5895f62e1706b173169db46b5978d80c43f6caec`
**Pre-registration**: `documents_v2/paper 4_DT/PAPER4_CHARTER.md` (LOCKED 2026-11-13; v1.3 adds H5 twin pre-reg, v1.2 pre-registered the 5-seed extension).
**Scope**: 5 seeds [42, 43, 44, 45, 46] x 3 models x 5 classes = 75 LOAO runs.
**v1.0 output**: archived at `results_v3_paper3/h8_verdict_v1_0_superseded/` - do NOT cite.
**v1.1 3-seed output**: archived at `results_v3_paper3/h8_verdict_v1_1_3seed_superseded/` - frozen reference.
**Surprises vs v1.0**: 10 per-pair tier flips (see `SURPRISES_v1_0_to_v1_1.md`).
**Surprises v1.1 3-seed vs v1.3 5-seed**: 7 per-pair tier flips (see `SURPRISES_v1_1_3seed_to_v1_3_5seed.md`).

---

## H1 — Safety view (TRACE-MoE `caught_any` ≥ 0.95)

**Overall**: **`SUPPORTED (strong, overall)`**
- Per-class: {'SUPPORTED (strong)': 5, 'SUPPORTED (preliminary)': 0, 'INCONCLUSIVE': 0, 'NOT SUPPORTED': 0}

## H2 — Energy AUROC > MSP AUROC

**Primary (TRACE-MoE)**: **`NOT SUPPORTED`**

Per-model breakdown:
- `trace_moe`: **NOT SUPPORTED** (SUPPORTED 0, INCONCLUSIVE 1, NOT 3)
- `transformer`: **MIXED** (SUPPORTED 0, INCONCLUSIVE 2, NOT 2)
- `bilstm_dnn`: **NOT SUPPORTED** (SUPPORTED 0, INCONCLUSIVE 0, NOT 4)

## H3 — TRACE-MoE energy AUROC > each baseline

Per-baseline breakdown:
- vs `transformer`: **SUPPORTED (preliminary)** (SUPPORTED 2, INCONCLUSIVE 1, NOT 1)
- vs `bilstm_dnn`: **SUPPORTED (strong)** (SUPPORTED 4, INCONCLUSIVE 1, NOT 0)

## H4 — Closed-set degradation ≤ 10 pt (v1.1 tightened from 15 pt)

**Overall**: **`INCONCLUSIVE (overall; ≥3 pairs inconclusive at 5-seed scope)`**
- Breakdown: {'SUPPORTED': 11, 'INCONCLUSIVE': 4, 'NOT SUPPORTED': 0}

## ESA1 — Calibration quality

- Target false-alarm rate (95% coverage): 0.0500
- Observed overall mean FAR across 45 runs: **0.0463**

## ESA2 — DEFERRED

Per-sample energy not saved in `predictions.npz`. See `ESA2_DEFERRED.md` for 4 resolution options (Option B recommended: post-hoc energy recompute from `model.pt`).

---

## INCONCLUSIVE pairs (any pair where CI straddles the verdict margin)

- Total: 9 pairs

| Hypothesis | Pair | Reason |
|---|---|---|
| H2 | trace_moe × TCP_IP-DoS-UDP | mean_diff=-0.1155, CI=[-0.2388, +0.0044] includes 0 |
| H2 | transformer × Recon-VulScan | mean_diff=-0.0668, CI=[-0.1951, +0.0615] includes 0 |
| H2 | transformer × MQTT-Malformed_Data | mean_diff=-0.0346, CI=[-0.1186, +0.0124] includes 0 |
| H3 | TRACE-MoE vs transformer × TCP_IP-DoS-UDP | mean_diff=-0.0888, CI=[-0.4373, +0.2596] includes 0 |
| H3 | TRACE-MoE vs bilstm_dnn × TCP_IP-DoS-UDP | mean_diff=-0.2150, CI=[-0.4467, +0.0554] includes 0 |
| H4 | bilstm_dnn × Recon-VulScan | mean_degr=+0.0680, CI=[-0.0006, +0.1497] straddles 0.10 (v1.1 threshold) |
| H4 | bilstm_dnn × MQTT-Malformed_Data | mean_degr=+0.0523, CI=[-0.0000, +0.1227] straddles 0.10 (v1.1 threshold) |
| H4 | bilstm_dnn × TCP_IP-DoS-UDP | mean_degr=+0.0827, CI=[+0.0011, +0.1653] straddles 0.10 (v1.1 threshold) |
| H4 | bilstm_dnn × MQTT-DDoS-Publish_Flood | mean_degr=+0.0635, CI=[-0.0186, +0.1505] straddles 0.10 (v1.1 threshold) |

---

## Files written

- `per_seed_tables.csv` — raw 75-row long table (5 seeds × 3 models × 5 classes)
- `H1_safety_view.{csv,md}`
- `H2_energy_vs_msp.{csv,md}`
- `H3_trace_moe_vs_baselines.{csv,md}`
- `H4_closed_set_degradation.{csv,md}`
- `ESA1_calibration.{csv,md}`
- `ESA2_DEFERRED.md`
- `SURPRISES_v1_0_to_v1_1.md` - tier flips introduced by Charter v1.1
- `SURPRISES_v1_1_3seed_to_v1_3_5seed.md` - tier flips from seed extension per Charter v1.2
- `VERDICT_SUMMARY_v1_3_5seed.md` (this file)
- `verdict.json` (machine-readable summary)
