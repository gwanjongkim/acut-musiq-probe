# Benchmark Summary — A-CUT MUSIQ Probe & Reference Benchmark

## Overview
- **Repository**: `acut-musiq-probe`
- **Role in A-CUT**: Reference Benchmark & Lightweight Mobile Probe Study (Negative Result for 1,024-row local probes)
- **Task**: Multi-Scale Transformer IQA Probe & Sanity Check

## Evaluated Metrics

| Model / Variant | Dataset | SRCC | PLCC | Notes |
| :--- | :---: | :---: | :---: | :--- |
| **Official Kaggle MUSIQ (`spaq`)** | SPAQ | **0.9460** | **0.9482** | Heavy multi-scale transformer reference |
| **Official Kaggle MUSIQ (`koniq`)** | KonIQ-10k | **0.9275** | **0.9389** | Heavy multi-scale transformer reference |
| **Official Kaggle MUSIQ (`paq2piq`)** | FLIVE | 0.4815 | 0.5412 | Cross-domain drop on FLIVE |
| **Local MUSIQ Probe1024 (1.41 MB)** | 1,024-row probes | Low / Underfit | - | Rejected for mobile production |

## Key Engineering & Audit Findings

- **Clear Lineage Separation (2026-07-11 Audit)**: Official Kaggle MUSIQ achieves `0.9460` (SPAQ) and `0.9275` (KonIQ-10k) using full multi-scale hash-grid positional encodings, whereas the 1.41 MB local `musiq_*_probe1024_fp16.tflite` models are tiny reduced-capacity probes that do not reproduce official MUSIQ accuracy.

## Evidence Files in `results/`
All metric tables, per-sample predictions, parity checks, and audit reports backing the numbers above are stored directly in the [`results/`](../results/) directory of this repository.
