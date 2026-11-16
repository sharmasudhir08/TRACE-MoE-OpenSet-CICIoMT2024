# H2 — Energy abstention vs MSP AUROC

**Charter rule**: paired bootstrap 95% CI of (energy_auroc − msp_auroc).
- SUPPORTED: CI excludes 0 AND mean > 0
- NOT SUPPORTED: CI excludes 0 AND mean < 0
- INCONCLUSIVE: CI includes 0 (CI-wider-than-margin at 5-seed scope)

**Per-model overall**:
- `trace_moe`: **NOT SUPPORTED** (SUPPORTED 0, INC 1, NOT 3)
- `transformer`: **MIXED** (SUPPORTED 0, INC 2, NOT 2)
- `bilstm_dnn`: **NOT SUPPORTED** (SUPPORTED 0, INC 0, NOT 4)

**Primary H2 answer (for TRACE-MoE)**: NOT SUPPORTED

## Per (model × class) pairs

| Model | Class | diff_s42 | diff_s43 | diff_s44 | diff_s45 | diff_s46 | mean_diff | CI 95% | Verdict |
|---|---|---|---|---|---|---|---|---|---|
| trace_moe | ARP_Spoofing | -0.0054 | +0.0145 | -0.0173 | +0.0275 | +0.0025 | +0.0044 | [-0.0086, +0.0183] | NOT SUPPORTED |
| trace_moe | Recon-VulScan | -0.0029 | -0.0008 | -0.0177 | +0.0071 | -0.0008 | -0.0030 | [-0.0110, +0.0035] | NOT SUPPORTED |
| trace_moe | MQTT-Malformed_Data | +0.0014 | -0.0023 | +0.0025 | -0.0108 | +0.0062 | -0.0006 | [-0.0059, +0.0038] | NOT SUPPORTED |
| trace_moe | TCP_IP-DoS-UDP | -0.3558 | -0.1614 | +0.0348 | +0.0475 | -0.1425 | -0.1155 | [-0.2388, +0.0044] | INCONCLUSIVE |
| trace_moe | MQTT-DDoS-Publish_Flood | +0.1269 | +0.5230 | +0.1540 | -0.1243 | +0.1496 | +0.1658 | [-0.0147, +0.3700] | SUPPORTED (preliminary) |
| transformer | ARP_Spoofing | +0.0075 | -0.0343 | -0.0068 | +0.0282 | +0.0077 | +0.0005 | [-0.0178, +0.0171] | NOT SUPPORTED |
| transformer | Recon-VulScan | +0.0885 | -0.2576 | -0.2408 | +0.0545 | +0.0215 | -0.0668 | [-0.1951, +0.0615] | INCONCLUSIVE |
| transformer | MQTT-Malformed_Data | +0.0032 | -0.0025 | -0.1999 | +0.0191 | +0.0072 | -0.0346 | [-0.1186, +0.0124] | INCONCLUSIVE |
| transformer | TCP_IP-DoS-UDP | +0.0042 | -0.2209 | +0.2045 | +0.3073 | +0.0336 | +0.0657 | [-0.0858, +0.2261] | SUPPORTED (preliminary) |
| transformer | MQTT-DDoS-Publish_Flood | -0.0681 | -0.0561 | -0.4497 | -0.2138 | -0.3756 | -0.2327 | [-0.3729, -0.0948] | NOT SUPPORTED |
| bilstm_dnn | ARP_Spoofing | -0.0715 | -0.1333 | -0.2950 | -0.1183 | -0.1405 | -0.1517 | [-0.2288, -0.0977] | NOT SUPPORTED |
| bilstm_dnn | Recon-VulScan | -0.0503 | -0.2597 | -0.4031 | -0.1745 | -0.0371 | -0.1850 | [-0.3039, -0.0699] | NOT SUPPORTED |
| bilstm_dnn | MQTT-Malformed_Data | -0.0727 | -0.1642 | -0.1211 | -0.0526 | -0.1697 | -0.1160 | [-0.1578, -0.0743] | NOT SUPPORTED |
| bilstm_dnn | TCP_IP-DoS-UDP | -0.3448 | -0.0211 | -0.0091 | +0.0024 | -0.1164 | -0.0978 | [-0.2297, -0.0069] | NOT SUPPORTED |
| bilstm_dnn | MQTT-DDoS-Publish_Flood | +0.0446 | +0.4239 | +0.0488 | -0.3339 | -0.0965 | +0.0174 | [-0.1915, +0.2439] | SUPPORTED (preliminary) |