# Data Access

## Source

CICIoMT2024 (Wi-Fi and MQTT subset) is a multi-protocol IoMT attack dataset
introduced by Dadkhah, Pinto Neto, Ferreira, Molokwu, Sadeghi, and Ghorbani,
"CICIoMT2024: Attack Vectors in Healthcare devices, A Multi-Protocol Dataset
for Assessing IoMT Device Security," *Internet of Things*, volume 28, 2024,
article 101351. DOI: `10.1016/j.iot.2024.101351`.

A copy is also distributed via IEEE DataPort under DOI `10.21227/tq0p-ag21`.
Obtain the raw CSV files from either source directly; this repository does
not redistribute the raw dataset, consistent with the dataset's own license
terms.

## What this study uses

The Wi-Fi and MQTT subset only (not the Bluetooth subset). The official,
file-level train/test split as distributed by the dataset's authors, not a
row-level random split (Section 4.1 of the manuscript). Nineteen fine-grained
attack-or-benign classes, grouped into six coarse categories and a binary
Benign-versus-Attack label.

## Expected local layout

The training pipeline (`scripts/07_unknown_attacks.py` and the shared
loading code under `src/trace_iomt/data/`, not included in this repository;
see the parent project) expects the official training and test CSV files
under a single directory, configured via `paths.ciciomt_csv_dir` in
`configs/default.yaml`. Place the downloaded CSVs so that path resolves, or
override it with `--set paths.ciciomt_csv_dir=/your/path` when invoking
`07_unknown_attacks.py`.

## Rebuilding the preprocessing cache

Feature scaling statistics are fit on training rows only and duplicate
windows are removed before training (manuscript Section 4.1); both are
handled automatically by the data-loading code the first time
`07_unknown_attacks.py` runs against a given configuration, and the result is
cached to speed up subsequent runs. No separate manual preprocessing step is
required beyond pointing the config at the raw CSVs. The cache itself is not
included in this repository (large; trivially reproducible from the raw CSVs
plus the scripts here).

## What this repository does NOT include, and why

| Not included | Why |
|---|---|
| Raw CICIoMT2024 CSV files | Publicly available from the sources above under their own license; not ours to redistribute |
| Preprocessed/windowed caches | Large; deterministically reproducible from the raw CSVs plus `configs/` and the (externally hosted) loading code |
| Model checkpoints (`model.pt`, 45 of them) | Large; reproducible by re-running `scripts/07_unknown_attacks.py`; consider a separate Zenodo deposit if a citable, fixed copy is wanted |
| Per-run `predictions.npz` | Large; contains per-sample softmax outputs for all three classification heads per run |
| Per-run training logs (`history.csv`) | Author-archive material, not needed to verify the manuscript's reported numbers |
