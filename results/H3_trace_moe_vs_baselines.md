# H3 — TRACE-MoE energy AUROC vs baselines

**Charter rule**: paired bootstrap of (trace_moe.energy_auroc − baseline.energy_auroc).
- SUPPORTED (per-baseline overall): ≥ 3 of 5 class pairs SUPPORTED
- NOT SUPPORTED (per-baseline overall): ≥ 3 of 5 class pairs NOT SUPPORTED
- INCONCLUSIVE (per-baseline overall): ≥ 3 of 5 class pairs INCONCLUSIVE
- MIXED (per-baseline overall): otherwise

**Per-baseline overall**:
- vs `transformer`: **SUPPORTED (preliminary)** (SUPPORTED 2, INC 1, NOT 1)
- vs `bilstm_dnn`: **SUPPORTED (strong)** (SUPPORTED 4, INC 1, NOT 0)

## Per (baseline × class) pairs

| Baseline | Class | diff_s42 | diff_s43 | diff_s44 | diff_s45 | diff_s46 | mean_diff | CI 95% | Verdict |
|---|---|---|---|---|---|---|---|---|---|
| transformer | ARP_Spoofing | -0.0034 | +0.0310 | +0.0009 | -0.0070 | -0.0010 | +0.0041 | [-0.0047, +0.0181] | NOT SUPPORTED |
| transformer | Recon-VulScan | -0.0125 | +0.3258 | +0.3058 | +0.0145 | +0.0089 | +0.1285 | [+0.0014, +0.2584] | SUPPORTED |
| transformer | MQTT-Malformed_Data | +0.0049 | +0.0106 | +0.2386 | -0.0182 | -0.0011 | +0.0470 | [-0.0090, +0.1450] | SUPPORTED (preliminary) |
| transformer | TCP_IP-DoS-UDP | -0.6462 | +0.0152 | +0.2791 | -0.4546 | +0.3624 | -0.0888 | [-0.4373, +0.2596] | INCONCLUSIVE |
| transformer | MQTT-DDoS-Publish_Flood | +0.4025 | +0.7082 | +0.5011 | +0.2257 | +0.2492 | +0.4173 | [+0.2704, +0.5750] | SUPPORTED |
| bilstm_dnn | ARP_Spoofing | +0.0801 | +0.4102 | +0.5554 | +0.1044 | +0.1534 | +0.2607 | [+0.1045, +0.4362] | SUPPORTED |
| bilstm_dnn | Recon-VulScan | +0.1585 | +0.3973 | +0.5703 | +0.3323 | +0.1325 | +0.3182 | [+0.1829, +0.4535] | SUPPORTED |
| bilstm_dnn | MQTT-Malformed_Data | +0.0882 | +0.2019 | +0.2420 | +0.0398 | +0.2046 | +0.1553 | [+0.0824, +0.2190] | SUPPORTED |
| bilstm_dnn | TCP_IP-DoS-UDP | -0.2774 | -0.2411 | -0.2360 | -0.5854 | +0.2651 | -0.2150 | [-0.4467, +0.0554] | INCONCLUSIVE |
| bilstm_dnn | MQTT-DDoS-Publish_Flood | +0.1314 | +0.2135 | +0.4957 | +0.1521 | +0.1137 | +0.2213 | [+0.1285, +0.3629] | SUPPORTED |