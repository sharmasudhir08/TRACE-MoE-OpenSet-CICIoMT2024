# ESA1 — Reject-threshold calibration quality

**Target coverage**: 0.95 → target `known_false_alarm_rate` = 0.05.

**Report** (direction-only; no formal verdict per Charter):
- Overall mean known_false_alarm_rate across 75 runs: 0.0463

## Per (model × class)

| Model | Class | far_s42 | far_s43 | far_s44 | far_s45 | far_s46 | mean | dev vs 0.05 | CI 95% |
|---|---|---|---|---|---|---|---|---|---|
| trace_moe | ARP_Spoofing | 0.0458 | 0.0399 | 0.0407 | 0.0451 | 0.0448 | 0.0432 | -0.0068 | [-0.0089, -0.0047] |
| trace_moe | Recon-VulScan | 0.0455 | 0.0400 | 0.0353 | 0.0421 | 0.0406 | 0.0407 | -0.0093 | [-0.0123, -0.0066] |
| trace_moe | MQTT-Malformed_Data | 0.0412 | 0.0403 | 0.0405 | 0.0330 | 0.0425 | 0.0395 | -0.0105 | [-0.0139, -0.0083] |
| trace_moe | TCP_IP-DoS-UDP | 0.0447 | 0.0446 | 0.0367 | 0.0382 | 0.0396 | 0.0408 | -0.0092 | [-0.0121, -0.0064] |
| trace_moe | MQTT-DDoS-Publish_Flood | 0.0451 | 0.0408 | 0.0418 | 0.0418 | 0.0380 | 0.0415 | -0.0085 | [-0.0105, -0.0064] |
| transformer | ARP_Spoofing | 0.0436 | 0.0391 | 0.0331 | 0.0619 | 0.0549 | 0.0465 | -0.0035 | [-0.0124, +0.0060] |
| transformer | Recon-VulScan | 0.0420 | 0.0628 | 0.0373 | 0.0428 | 0.0422 | 0.0454 | -0.0046 | [-0.0107, +0.0046] |
| transformer | MQTT-Malformed_Data | 0.0432 | 0.0428 | 0.0322 | 0.0426 | 0.0428 | 0.0407 | -0.0093 | [-0.0136, -0.0070] |
| transformer | TCP_IP-DoS-UDP | 0.0429 | 0.0401 | 0.0297 | 0.0443 | 0.0419 | 0.0398 | -0.0102 | [-0.0153, -0.0068] |
| transformer | MQTT-DDoS-Publish_Flood | 0.0429 | 0.0441 | 0.0442 | 0.0415 | 0.0428 | 0.0431 | -0.0069 | [-0.0077, -0.0061] |
| bilstm_dnn | ARP_Spoofing | 0.0454 | 0.0703 | 0.0567 | 0.0452 | 0.0427 | 0.0520 | +0.0020 | [-0.0058, +0.0121] |
| bilstm_dnn | Recon-VulScan | 0.0304 | 0.0415 | 0.0260 | 0.0239 | 0.1172 | 0.0478 | -0.0022 | [-0.0239, +0.0334] |
| bilstm_dnn | MQTT-Malformed_Data | 0.1287 | 0.0384 | 0.0275 | 0.0535 | 0.0384 | 0.0573 | +0.0073 | [-0.0160, +0.0434] |
| bilstm_dnn | TCP_IP-DoS-UDP | 0.0306 | 0.0707 | 0.0396 | 0.0422 | 0.0363 | 0.0439 | -0.0061 | [-0.0158, +0.0081] |
| bilstm_dnn | MQTT-DDoS-Publish_Flood | 0.0522 | 0.0361 | 0.2047 | 0.0322 | 0.0340 | 0.0718 | +0.0218 | [-0.0163, +0.0897] |