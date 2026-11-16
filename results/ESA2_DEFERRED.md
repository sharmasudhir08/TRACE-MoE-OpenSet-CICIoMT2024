# ESA2 — Spearman ρ between energy and (1 − MSP): DEFERRED

Per Charter §Exploratory Supplementary Analyses, ESA2 requires per-sample energy
scores for the held-out (unknown) attack subset of each test window.

**Blocker**: `results_v3_paper3/zero_day/<run>/predictions.npz` does NOT contain
per-sample energy values. Keys present (verified 2026-10-14):

  y_true_label2, y_pred_label2, proba_label2,
  y_true_label6, y_pred_label6, proba_label6,
  y_true_label19, y_pred_label19, proba_label19,
  val_y_true_label2, val_y_pred_label2, val_proba_label2,
  val_y_true_label6, val_y_pred_label6, val_proba_label6,
  val_y_true_label19, val_y_pred_label19, val_proba_label19,
  route

Energy = -logsumexp(logits) cannot be recovered from softmax probabilities alone
(the normalisation constant is lost in the softmax). MSP can be recovered as
`proba_label19.max(axis=1)` but energy requires either the raw logits or a
re-inference pass that saves energy.

**Resolution options** (none executed; await user decision):

- **Option A** — Re-run Script 07 for the 45 LOAO runs with an added energy-export
  flag. Compute cost: ~2-3 h on your i7-12700H / RTX 3050 since inference-only
  (no retraining); the model.pt checkpoints are already on disk. This produces
  per-sample energy arrays and enables ESA2 proper.

- **Option B** — Build a post-hoc `scripts/paper4_recompute_energy.py` that loads
  each saved model.pt, performs inference on the test windows, extracts logits,
  computes energy, and saves per-run `energy_test.npy`. Then re-run this
  verdict script with ESA2 enabled. Compute cost: similar to Option A, ~2-3 h.

- **Option C** — Replace ESA2 with a weaker proxy using `-log(max_proba)` as a
  "softmax-energy" surrogate. This is TRIVIALLY correlated with (1 − MSP) by
  construction (ρ ≈ 1.0) and therefore DOES NOT answer ESA2's question. Not
  recommended; would be a vacuous ESA2 report.

- **Option D** — Mark ESA2 as "deferred to future work" in the Paper 4
  manuscript. Charter already permits this at §ESA2.

**Recommended**: Option B (post-hoc per-run energy recompute). It produces real
ESA2 numbers from the existing checkpoints without re-training.

Decision pending user approval.
