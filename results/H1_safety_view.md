# H1 — Safety-view detection rate (TRACE-MoE caught_any ≥ 0.95)

**Charter rule**: four-tier verdict.
- SUPPORTED (strong): mean ≥ 0.95 AND CI lower bound ≥ 0.90
- SUPPORTED (preliminary): mean ≥ 0.95, CI lower bound < 0.90
- INCONCLUSIVE: mean < 0.95, CI straddles 0.95
- NOT SUPPORTED: CI upper bound < 0.95

**Overall verdict**: `SUPPORTED (strong, overall)`

## Per class (TRACE-MoE caught_any)

| Class | seed42 | seed43 | seed44 | seed45 | seed46 | mean | CI 95% | CI width | Verdict |
|---|---|---|---|---|---|---|---|---|---|
| ARP_Spoofing | 0.9902 | 0.9942 | 0.9167 | 0.9983 | 0.9815 | 0.9762 | [0.9460, 0.9950] | 0.0490 | SUPPORTED (strong) |
| Recon-VulScan | 0.9990 | 0.9961 | 0.9892 | 1.0000 | 1.0000 | 0.9969 | [0.9927, 0.9998] | 0.0071 | SUPPORTED (strong) |
| MQTT-Malformed_Data | 1.0000 | 0.9059 | 1.0000 | 0.9792 | 1.0000 | 0.9770 | [0.9394, 1.0000] | 0.0606 | SUPPORTED (strong) |
| TCP_IP-DoS-UDP | 1.0000 | 1.0000 | 1.0000 | 1.0000 | 1.0000 | 1.0000 | [1.0000, 1.0000] | 0.0000 | SUPPORTED (strong) |
| MQTT-DDoS-Publish_Flood | 1.0000 | 1.0000 | 1.0000 | 1.0000 | 1.0000 | 1.0000 | [1.0000, 1.0000] | 0.0000 | SUPPORTED (strong) |