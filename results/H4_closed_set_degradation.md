# H4 — Closed-set macro-F1 degradation ≤ 10 pt (v1.1 tightened from 15 pt)

**Charter rule**: Paper 1 full-model baseline (recomputed over the SAME 18 non-held-out classes per pair) minus Phase 3(c) `known_classes_macro_f1`. Positive degradation = Phase 3(c) worse than Paper 1 baseline.
- SUPPORTED (per-pair): CI upper bound ≤ 0.10 AND mean ≤ 0.10
- NOT SUPPORTED (per-pair): CI lower bound > 0.10 AND mean > 0.10
- INCONCLUSIVE (per-pair): CI straddles 0.10

**Rationale for 10 pt threshold** (v1.1): 10 pt is the common open-set
robustness convention and a deployment-acceptable macro-F1 degradation bar
for IoMT NIDS.

**Overall verdict**: `INCONCLUSIVE (overall; ≥3 pairs inconclusive at 5-seed scope)`
- Breakdown: SUPPORTED 11, INC 4, NOT 0

## Per (model × class) pairs

| Model | Class | p1_s42 | p1_s43 | p1_s44 | p1_s45 | p1_s46 | p3c_s42 | p3c_s43 | p3c_s44 | p3c_s45 | p3c_s46 | mean_degr | CI 95% | Verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| trace_moe | ARP_Spoofing | 0.8313 | 0.8293 | 0.8330 | 0.8315 | 0.8259 | 0.8055 | 0.8000 | 0.7990 | 0.8448 | 0.8548 | +0.0094 | [-0.0141, +0.0305] | SUPPORTED |
| trace_moe | Recon-VulScan | 0.8496 | 0.8509 | 0.8541 | 0.8433 | 0.8364 | 0.8468 | 0.8140 | 0.7832 | 0.8467 | 0.8479 | +0.0191 | [-0.0054, +0.0476] | SUPPORTED |
| trace_moe | MQTT-Malformed_Data | 0.8133 | 0.8122 | 0.8211 | 0.8082 | 0.8010 | 0.8042 | 0.7694 | 0.7787 | 0.8108 | 0.8130 | +0.0159 | [-0.0040, +0.0359] | SUPPORTED |
| trace_moe | TCP_IP-DoS-UDP | 0.8070 | 0.8060 | 0.8149 | 0.8026 | 0.7949 | 0.7906 | 0.7595 | 0.7516 | 0.8065 | 0.7935 | +0.0247 | [+0.0022, +0.0476] | SUPPORTED |
| trace_moe | MQTT-DDoS-Publish_Flood | 0.8519 | 0.8511 | 0.8599 | 0.8475 | 0.8398 | 0.8537 | 0.8260 | 0.8218 | 0.8747 | 0.8587 | +0.0031 | [-0.0188, +0.0250] | SUPPORTED |
| transformer | ARP_Spoofing | 0.8183 | 0.8130 | 0.8157 | 0.7846 | 0.8051 | 0.8203 | 0.7920 | 0.8007 | 0.8404 | 0.8394 | -0.0112 | [-0.0374, +0.0140] | SUPPORTED |
| transformer | Recon-VulScan | 0.8377 | 0.8222 | 0.8260 | 0.8013 | 0.8157 | 0.8356 | 0.7749 | 0.8028 | 0.8146 | 0.8323 | +0.0086 | [-0.0115, +0.0304] | SUPPORTED |
| transformer | MQTT-Malformed_Data | 0.8056 | 0.7920 | 0.7962 | 0.7691 | 0.7815 | 0.7928 | 0.7537 | 0.7676 | 0.8080 | 0.7925 | +0.0060 | [-0.0198, +0.0293] | SUPPORTED |
| transformer | TCP_IP-DoS-UDP | 0.7948 | 0.7798 | 0.7832 | 0.7572 | 0.7726 | 0.7839 | 0.7352 | 0.7609 | 0.7945 | 0.7655 | +0.0095 | [-0.0166, +0.0311] | SUPPORTED |
| transformer | MQTT-DDoS-Publish_Flood | 0.8397 | 0.8248 | 0.8281 | 0.8021 | 0.8176 | 0.8390 | 0.8094 | 0.8055 | 0.8475 | 0.8423 | -0.0063 | [-0.0291, +0.0153] | SUPPORTED |
| bilstm_dnn | ARP_Spoofing | 0.7504 | 0.7474 | 0.7484 | 0.7545 | 0.7487 | 0.7442 | 0.6390 | 0.6451 | 0.7496 | 0.7441 | +0.0455 | [+0.0050, +0.0867] | SUPPORTED |
| bilstm_dnn | Recon-VulScan | 0.7640 | 0.7577 | 0.7594 | 0.7663 | 0.7600 | 0.7611 | 0.5550 | 0.6222 | 0.7630 | 0.7661 | +0.0680 | [-0.0006, +0.1497] | INCONCLUSIVE |
| bilstm_dnn | MQTT-Malformed_Data | 0.7343 | 0.7295 | 0.7301 | 0.7360 | 0.7313 | 0.7362 | 0.5519 | 0.6472 | 0.7336 | 0.7305 | +0.0523 | [-0.0000, +0.1227] | INCONCLUSIVE |
| bilstm_dnn | TCP_IP-DoS-UDP | 0.7103 | 0.7042 | 0.7058 | 0.7127 | 0.7065 | 0.7070 | 0.4960 | 0.5049 | 0.7119 | 0.7063 | +0.0827 | [+0.0011, +0.1653] | INCONCLUSIVE |
| bilstm_dnn | MQTT-DDoS-Publish_Flood | 0.7543 | 0.7485 | 0.7501 | 0.7534 | 0.7502 | 0.7671 | 0.5785 | 0.5496 | 0.7723 | 0.7713 | +0.0635 | [-0.0186, +0.1505] | INCONCLUSIVE |