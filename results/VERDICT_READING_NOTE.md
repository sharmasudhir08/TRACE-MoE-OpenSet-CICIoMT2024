# VERDICT_READING_NOTE.md

**Date**: 2026-11-15  
**Author**: Sudhir Kumar Sharma  
**Purpose**: Records the strict-reading decision for H2/H3 per-pair verdicts and its effect on overall verdicts.

---

## Charter v1.1 Per-Pair Rule (H2 and H3)

The Charter v1.1 (SHA256 `9102ca7d47a443c2bc74301cf4ff8a98f1996f7f69c3b620f03c5afe281cf308`) defines four per-pair verdict tiers for H2 and H3:

| Tier | Condition |
|---|---|
| SUPPORTED (bare) | CI excludes 0 AND mean > 0 |
| SUPPORTED (preliminary) | mean > 0 AND CI width > 0.10 (CI may straddle zero) |
| INCONCLUSIVE | CI includes 0 AND CI width > 0.10 AND [mean <= 0 or no positive direction] |
| NOT SUPPORTED | CI excludes 0 AND mean < 0, OR (CI includes 0 AND CI width <= 0.10 — narrow null) |

## The Overlap

When BOTH apply simultaneously: (1) CI straddles zero AND (2) mean > 0 AND (3) CI width > 0.10, then both SUPPORTED (preliminary) and INCONCLUSIVE conditions are triggered.

## Two Readings

**Code reading** (deposited verdict files): Resolves the overlap in favour of SUPPORTED (preliminary), following the Charter's condition order. This is what the files `H2_energy_vs_msp.md` and `H3_trace_moe_vs_baselines.md` report.

**Strict reading** (adopted in manuscript `paper4_manuscript_v2.2_new.docx`): A CI straddling zero is sufficient to classify a pair as inconclusive regardless of the sign of the point estimate. Such pairs are labelled **Inconclusive (positive point estimate)** in the manuscript.

## The Four Affected Pairs

| Hypothesis | Model | Held-out class | mean | 95% CI | Code label | Manuscript label |
|---|---|---|---|---|---|---|
| H2 | TRACE-MoE | MQTT-DDoS-Publish_Flood | +0.1658 | [-0.0147, +0.3700] | SUPPORTED (preliminary) | Inconclusive (positive point estimate) |
| H2 | Transformer | TCP_IP-DoS-UDP | +0.0657 | [-0.0858, +0.2261] | SUPPORTED (preliminary) | Inconclusive (positive point estimate) |
| H2 | BiLSTM-DNN | MQTT-DDoS-Publish_Flood | +0.0174 | [-0.1915, +0.2439] | SUPPORTED (preliminary) | Inconclusive (positive point estimate) |
| H3 | Transformer vs TRACE-MoE | MQTT-Malformed_Data | +0.0470 | [-0.0090, +0.1450] | SUPPORTED (preliminary) | Inconclusive (positive point estimate) |

## Effect on Overall Verdicts

| Level | Old (code reading) | New (strict reading) |
|---|---|---|
| H2 Transformer overall | MIXED | INCONCLUSIVE |
| H3 TRACE-MoE vs Transformer overall | SUPPORTED (preliminary) | MIXED |
| Total inconclusive pairs (H1-H4) | 9 | 13 |
| TCP/IP DoS-UDP inconclusive pairs | 4 | 5 |

## Why the Manuscript Uses Strict Reading

A CI that straddles zero means the data are consistent with zero or negative difference, regardless of where the point estimate falls. Labelling such a pair "supported" — even with the "(preliminary)" qualifier — risks overstating the evidence. The strict reading is the more conservative and scientifically honest choice.

---

**Released verdict files** (`H2_energy_vs_msp.md`, `H3_trace_moe_vs_baselines.md`): carry the code labels. Any downstream use of these files should refer to this note for the manuscript-adopted labels.
