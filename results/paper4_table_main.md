# Paper 4 Main Verdict Table (4-panel, 5-seed aggregation)

**Charter**: v1.3 (SHA-verified); statistical recipe v1.1; seed scope extended per v1.2; SHA256 `130767067f36261dca0370a12c418da70bf081a249ce380f6df613508f675a42`

**Source CSVs** (read-only inputs; byte-identical to the aggregator output recorded in verdict.json, generated 2026-11-13T23:53:42.501549+00:00):

- `H1_safety_view.csv` (5 pairs)
- `H2_energy_vs_msp.csv` (15 pairs)
- `H3_trace_moe_vs_baselines.csv` (10 pairs)
- `H4_closed_set_degradation.csv` (15 pairs)
- `ESA1_calibration.csv` (15 pairs, direction-only)

**Total verdict cells rendered**: 45 (= 5 + 15 + 10 + 15).

**Watch-item TCP_IP-DoS-UDP check**: 4 of 9 INCONCLUSIVE verdicts across H1-H4 involve TCP_IP-DoS-UDP as the held-out attack.

---

## Panel 1 of 4 — H1 safety-view detection rate (TRACE-MoE caught_any across 5 held-out classes x 3 seeds)

Rule: SUPPORTED (strong) if mean caught_any >= 0.95 AND CI lower bound >= 0.90.

| Held-out class | seed42 | seed43 | seed44 | mean | 95% CI | width | Verdict |
|---|---|---|---|---|---|---|---|
| ARP_Spoofing | 0.9902 | 0.9942 | 0.9167 | 0.9762 | [0.9460, 0.9950] | 0.0490 | SUPPORTED (strong) |
| Recon-VulScan | 0.9990 | 0.9961 | 0.9892 | 0.9969 | [0.9927, 0.9998] | 0.0071 | SUPPORTED (strong) |
| MQTT-Malformed_Data | 1.0000 | 0.9059 | 1.0000 | 0.9770 | [0.9394, 1.0000] | 0.0606 | SUPPORTED (strong) |
| TCP_IP-DoS-UDP | 1.0000 | 1.0000 | 1.0000 | 1.0000 | [1.0000, 1.0000] | 0.0000 | SUPPORTED (strong) |
| MQTT-DDoS-Publish_Flood | 1.0000 | 1.0000 | 1.0000 | 1.0000 | [1.0000, 1.0000] | 0.0000 | SUPPORTED (strong) |

H1 breakdown over 5 class pairs: SUPPORTED (strong) 5, SUPPORTED (preliminary) 0, INCONCLUSIVE 0, NOT SUPPORTED 0.

## Panel 2 of 4 — H2 energy AUROC minus MSP AUROC (3 models x 5 held-out classes = 15 pairs)

Rule: paired bootstrap 95% CI of (energy_auroc minus msp_auroc) across 3 seeds. Expected effect 0.05 AUROC, CI width margin 0.10 (= 2 x expected). 4-tier verdict per Charter v1.1.

| Model | Held-out class | diff s42 | diff s43 | diff s44 | mean_diff | 95% CI | width | Verdict |
|---|---|---|---|---|---|---|---|---|
| trace_moe | ARP_Spoofing | -0.0054 | 0.0145 | -0.0173 | 0.0044 | [-0.0086, 0.0183] | 0.0270 | NOT SUPPORTED (narrow null) |
| trace_moe | Recon-VulScan | -0.0029 | -0.0008 | -0.0177 | -0.0030 | [-0.0110, 0.0035] | 0.0145 | NOT SUPPORTED (narrow null) |
| trace_moe | MQTT-Malformed_Data | 0.0014 | -0.0023 | 0.0025 | -0.0006 | [-0.0059, 0.0038] | 0.0097 | NOT SUPPORTED (narrow null) |
| trace_moe | TCP_IP-DoS-UDP | -0.3558 | -0.1614 | 0.0348 | -0.1155 | [-0.2388, 0.0044] | 0.2433 | INCONCLUSIVE |
| trace_moe | MQTT-DDoS-Publish_Flood | 0.1269 | 0.5230 | 0.1540 | 0.1658 | [-0.0147, 0.3700] | 0.3847 | SUPPORTED (prelim) |
| transformer | ARP_Spoofing | 0.0075 | -0.0343 | -0.0068 | 0.0005 | [-0.0178, 0.0171] | 0.0348 | NOT SUPPORTED (narrow null) |
| transformer | Recon-VulScan | 0.0885 | -0.2576 | -0.2408 | -0.0668 | [-0.1951, 0.0615] | 0.2566 | INCONCLUSIVE |
| transformer | MQTT-Malformed_Data | 0.0032 | -0.0025 | -0.1999 | -0.0346 | [-0.1186, 0.0124] | 0.1310 | INCONCLUSIVE |
| transformer | TCP_IP-DoS-UDP | 0.0042 | -0.2209 | 0.2045 | 0.0657 | [-0.0858, 0.2261] | 0.3120 | SUPPORTED (prelim) |
| transformer | MQTT-DDoS-Publish_Flood | -0.0681 | -0.0561 | -0.4497 | -0.2327 | [-0.3729, -0.0948] | 0.2780 | NOT SUPPORTED (baseline wins) |
| bilstm_dnn | ARP_Spoofing | -0.0715 | -0.1333 | -0.2950 | -0.1517 | [-0.2288, -0.0977] | 0.1311 | NOT SUPPORTED (baseline wins) |
| bilstm_dnn | Recon-VulScan | -0.0503 | -0.2597 | -0.4031 | -0.1850 | [-0.3039, -0.0699] | 0.2340 | NOT SUPPORTED (baseline wins) |
| bilstm_dnn | MQTT-Malformed_Data | -0.0727 | -0.1642 | -0.1211 | -0.1160 | [-0.1578, -0.0743] | 0.0834 | NOT SUPPORTED (baseline wins) |
| bilstm_dnn | TCP_IP-DoS-UDP | -0.3448 | -0.0211 | -0.0091 | -0.0978 | [-0.2297, -0.0069] | 0.2228 | NOT SUPPORTED (baseline wins) |
| bilstm_dnn | MQTT-DDoS-Publish_Flood | 0.0446 | 0.4239 | 0.0488 | 0.0174 | [-0.1915, 0.2439] | 0.4354 | SUPPORTED (prelim) |

H2 breakdown for trace_moe: SUPPORTED (strong) 0, SUPPORTED (preliminary) 0, SUPPORTED 0, INCONCLUSIVE 1, NOT SUPPORTED (narrow null) 3, NOT SUPPORTED (baseline wins) 0.
H2 breakdown for transformer: SUPPORTED (strong) 0, SUPPORTED (preliminary) 0, SUPPORTED 0, INCONCLUSIVE 2, NOT SUPPORTED (narrow null) 1, NOT SUPPORTED (baseline wins) 1.
H2 breakdown for bilstm_dnn: SUPPORTED (strong) 0, SUPPORTED (preliminary) 0, SUPPORTED 0, INCONCLUSIVE 0, NOT SUPPORTED (narrow null) 0, NOT SUPPORTED (baseline wins) 4.

## Panel 3 of 4 — H3 TRACE-MoE energy AUROC minus baseline energy AUROC (2 baselines x 5 held-out classes = 10 pairs)

Rule: paired bootstrap 95% CI of (trace_moe.energy_auroc minus baseline.energy_auroc) across 3 seeds. Expected effect 0.05 AUROC, CI width margin 0.10. 4-tier verdict per Charter v1.1.

| Baseline | Held-out class | TRACE-MoE s42 | TRACE-MoE s43 | TRACE-MoE s44 | baseline s42 | baseline s43 | baseline s44 | mean_diff | 95% CI | width | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|
| transformer | ARP_Spoofing | 0.9818 | 0.9778 | 0.9685 | 0.9852 | 0.9468 | 0.9676 | 0.0041 | [-0.0047, 0.0181] | 0.0228 | NOT SUPPORTED (narrow null) |
| transformer | Recon-VulScan | 0.9686 | 0.9791 | 0.9523 | 0.9812 | 0.6533 | 0.6465 | 0.1285 | [0.0014, 0.2584] | 0.2570 | SUPPORTED |
| transformer | MQTT-Malformed_Data | 0.9870 | 0.9718 | 0.9831 | 0.9821 | 0.9612 | 0.7446 | 0.0470 | [-0.0090, 0.1450] | 0.1540 | SUPPORTED (prelim) |
| transformer | TCP_IP-DoS-UDP | 0.1971 | 0.6769 | 0.7480 | 0.8433 | 0.6617 | 0.4689 | -0.0888 | [-0.4373, 0.2596] | 0.6969 | INCONCLUSIVE |
| transformer | MQTT-DDoS-Publish_Flood | 0.4904 | 0.8673 | 0.9059 | 0.0880 | 0.1591 | 0.4048 | 0.4173 | [0.2704, 0.5750] | 0.3046 | SUPPORTED |
| bilstm_dnn | ARP_Spoofing | 0.9818 | 0.9778 | 0.9685 | 0.9017 | 0.5676 | 0.4131 | 0.2607 | [0.1045, 0.4362] | 0.3317 | SUPPORTED |
| bilstm_dnn | Recon-VulScan | 0.9686 | 0.9791 | 0.9523 | 0.8101 | 0.5818 | 0.3820 | 0.3182 | [0.1829, 0.4535] | 0.2706 | SUPPORTED |
| bilstm_dnn | MQTT-Malformed_Data | 0.9870 | 0.9718 | 0.9831 | 0.8988 | 0.7698 | 0.7411 | 0.1553 | [0.0824, 0.2190] | 0.1366 | SUPPORTED |
| bilstm_dnn | TCP_IP-DoS-UDP | 0.1971 | 0.6769 | 0.7480 | 0.4744 | 0.9179 | 0.9840 | -0.2150 | [-0.4467, 0.0554] | 0.5020 | INCONCLUSIVE |
| bilstm_dnn | MQTT-DDoS-Publish_Flood | 0.4904 | 0.8673 | 0.9059 | 0.3590 | 0.6538 | 0.4102 | 0.2213 | [0.1285, 0.3629] | 0.2344 | SUPPORTED |

H3 breakdown vs transformer: SUPPORTED (strong) 0, SUPPORTED (preliminary) 0, SUPPORTED 2, INCONCLUSIVE 1, NOT SUPPORTED (narrow null) 1, NOT SUPPORTED (baseline wins) 0.
H3 breakdown vs bilstm_dnn: SUPPORTED (strong) 0, SUPPORTED (preliminary) 0, SUPPORTED 4, INCONCLUSIVE 1, NOT SUPPORTED (narrow null) 0, NOT SUPPORTED (baseline wins) 0.

## Panel 4 of 4 — H4 closed-set macro-F1 degradation (3 models x 5 held-out classes = 15 pairs, 10 pt threshold)

Rule: Paper 1 full-model baseline (recomputed over the SAME 18 non-held-out classes per pair) minus Phase 3(c) known_classes_macro_f1. 3-tier verdict: SUPPORTED if CI upper <= 0.10, NOT SUPPORTED if CI lower > 0.10, else INCONCLUSIVE. 10 pt threshold tightened from 15 pt in Charter v1.1.

| Model | Held-out class | degr s42 | degr s43 | degr s44 | mean_degr | 95% CI | width | Verdict |
|---|---|---|---|---|---|---|---|---|
| trace_moe | ARP_Spoofing | 0.0258 | 0.0293 | 0.0340 | 0.0094 | [-0.0141, 0.0305] | 0.0446 | SUPPORTED |
| trace_moe | Recon-VulScan | 0.0028 | 0.0368 | 0.0708 | 0.0191 | [-0.0054, 0.0476] | 0.0530 | SUPPORTED |
| trace_moe | MQTT-Malformed_Data | 0.0090 | 0.0428 | 0.0424 | 0.0159 | [-0.0040, 0.0359] | 0.0399 | SUPPORTED |
| trace_moe | TCP_IP-DoS-UDP | 0.0164 | 0.0465 | 0.0633 | 0.0247 | [0.0022, 0.0476] | 0.0453 | SUPPORTED |
| trace_moe | MQTT-DDoS-Publish_Flood | -0.0018 | 0.0251 | 0.0381 | 0.0031 | [-0.0188, 0.0250] | 0.0437 | SUPPORTED |
| transformer | ARP_Spoofing | -0.0020 | 0.0210 | 0.0150 | -0.0112 | [-0.0374, 0.0140] | 0.0514 | SUPPORTED |
| transformer | Recon-VulScan | 0.0021 | 0.0474 | 0.0232 | 0.0086 | [-0.0115, 0.0304] | 0.0419 | SUPPORTED |
| transformer | MQTT-Malformed_Data | 0.0128 | 0.0383 | 0.0286 | 0.0060 | [-0.0198, 0.0293] | 0.0492 | SUPPORTED |
| transformer | TCP_IP-DoS-UDP | 0.0109 | 0.0446 | 0.0223 | 0.0095 | [-0.0166, 0.0311] | 0.0477 | SUPPORTED |
| transformer | MQTT-DDoS-Publish_Flood | 0.0007 | 0.0154 | 0.0226 | -0.0063 | [-0.0291, 0.0153] | 0.0444 | SUPPORTED |
| bilstm_dnn | ARP_Spoofing | 0.0061 | 0.1084 | 0.1034 | 0.0455 | [0.0050, 0.0867] | 0.0817 | SUPPORTED |
| bilstm_dnn | Recon-VulScan | 0.0029 | 0.2028 | 0.1372 | 0.0680 | [-0.0006, 0.1497] | 0.1503 | INCONCLUSIVE |
| bilstm_dnn | MQTT-Malformed_Data | -0.0020 | 0.1776 | 0.0829 | 0.0523 | [-0.0000, 0.1227] | 0.1227 | INCONCLUSIVE |
| bilstm_dnn | TCP_IP-DoS-UDP | 0.0034 | 0.2082 | 0.2009 | 0.0827 | [0.0011, 0.1653] | 0.1642 | INCONCLUSIVE |
| bilstm_dnn | MQTT-DDoS-Publish_Flood | -0.0128 | 0.1700 | 0.2006 | 0.0635 | [-0.0186, 0.1505] | 0.1691 | INCONCLUSIVE |

H4 breakdown for trace_moe: SUPPORTED 5, INCONCLUSIVE 0, NOT SUPPORTED 0.
H4 breakdown for transformer: SUPPORTED 5, INCONCLUSIVE 0, NOT SUPPORTED 0.
H4 breakdown for bilstm_dnn: SUPPORTED 1, INCONCLUSIVE 4, NOT SUPPORTED 0.

## ESA1 calibration summary (direction-only report, per Charter v1.1)

| | Target (95% coverage) | Observed overall mean across 15 (model x class) pairs |
|---|---|---|
| known_false_alarm_rate | 0.0500 | 0.0463 |

Per-pair observed FAR is in `ESA1_calibration.csv`. Overall calibration drift from target is 0.0037 absolute, i.e. empirical reject layer is slightly conservative.

## Verdict label disambiguation audit (presentation layer, no Charter rule change)

Cells relabeled from raw 'NOT SUPPORTED' (as stored in the aggregator CSV) to the finer presentation label (as rendered in Panels 2 and 3 above):

| Hypothesis | Pair | Raw (CSV) | Final (table) |
|---|---|---|---|
| H2 | trace_moe x ARP_Spoofing | NOT SUPPORTED | NOT SUPPORTED (narrow null) |
| H2 | trace_moe x Recon-VulScan | NOT SUPPORTED | NOT SUPPORTED (narrow null) |
| H2 | trace_moe x MQTT-Malformed_Data | NOT SUPPORTED | NOT SUPPORTED (narrow null) |
| H2 | transformer x ARP_Spoofing | NOT SUPPORTED | NOT SUPPORTED (narrow null) |
| H2 | transformer x MQTT-DDoS-Publish_Flood | NOT SUPPORTED | NOT SUPPORTED (baseline wins) |
| H2 | bilstm_dnn x ARP_Spoofing | NOT SUPPORTED | NOT SUPPORTED (baseline wins) |
| H2 | bilstm_dnn x Recon-VulScan | NOT SUPPORTED | NOT SUPPORTED (baseline wins) |
| H2 | bilstm_dnn x MQTT-Malformed_Data | NOT SUPPORTED | NOT SUPPORTED (baseline wins) |
| H2 | bilstm_dnn x TCP_IP-DoS-UDP | NOT SUPPORTED | NOT SUPPORTED (baseline wins) |
| H3 | vs transformer x ARP_Spoofing | NOT SUPPORTED | NOT SUPPORTED (narrow null) |

**Count across all 45 cells**: NOT SUPPORTED (narrow null) 5, NOT SUPPORTED (baseline wins) 5.

This audit list is the reviewer-citable artefact proving the sub-tagging is deterministic from the CSV data and the Charter v1.1 narrow-null rule, not post-hoc reinterpretation.

## Legend

**4-tier verdict scheme per Charter v1.1** (locked SHA `e1d29fc2b3278515579599bd5895f62e1706b173169db46b5978d80c43f6caec`):

- **SUPPORTED (strong)**: CI excludes zero AND tight (width <= margin for H2/H3) OR mean meets threshold with CI tight (for H1).
- **SUPPORTED (preliminary)**: mean is favourable but CI width exceeds margin; honest small-sample reporting.
- **SUPPORTED**: CI excludes zero (plain tier used for H4 where no strong/prelim split applies).
- **INCONCLUSIVE**: CI straddles the decision boundary AND is wide (> margin). Evidence insufficient at 3-seed scope.
- **NOT SUPPORTED (narrow null)**: CI contains zero AND width <= margin (0.10 for H2/H3). The effect is precise enough to say it is below the practical-significance threshold even though the point estimate may be of either sign.
- **NOT SUPPORTED (baseline wins)**: CI excludes zero in the negative direction (CI upper < 0) AND mean < 0. The baseline strictly outperforms TRACE-MoE on this pair.

Charter-faithful disambiguation note: v1.1 §Verdict tiers already distinguishes these two cases in text. The aggregator CSV collapses them to a single 'NOT SUPPORTED' label; this table restores the distinction at render time without altering any verdict rule or re-running aggregation. No Charter SHA bump is required.

**Per-hypothesis margins (locked in Charter v1.1)**:

| Hypothesis | Decision quantity | Threshold or margin | Direction |
|---|---|---|---|
| H1 | caught_any (TRACE-MoE) | mean >= 0.95 AND CI lower >= 0.90 for strong | higher better |
| H2 | energy_auroc minus msp_auroc | expected effect 0.05 AUROC; CI width margin 0.10 (= 2 x expected) | higher better |
| H3 | trace_moe.energy_auroc minus baseline.energy_auroc | expected effect 0.05 AUROC; CI width margin 0.10 | higher better |
| H4 | Paper 1 baseline minus Phase 3(c) known_classes_macro_f1 | 10 pt threshold (tightened from 15 pt in v1.1) | lower better |

All CI columns are bootstrap 95% CIs over 5 seeds (10,000 resamples, fixed RNG seed per Charter).
