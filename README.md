# A-CUT MUSIQ Probe & Reference Benchmark

> **A-CUT Multi-Scale Image Quality Transformer (MUSIQ) — Official Kaggle Reference Benchmark vs Lightweight Mobile Probes**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Project: A-CUT](https://img.shields.io/badge/Project-A--CUT%20Capstone-success.svg)](https://github.com/gwanjongkim/photo_score_project)

## 1. Overview

- **Role in A-CUT**: Reference Benchmark & Lightweight Mobile Probe Study (Negative Result for 1,024-row local probes)
- **Task**: Multi-Scale Transformer IQA Probe & Sanity Check
- **Architecture**: 1) Official Google Research MUSIQ (`spaq`, `koniq`, `paq2piq` TF-Hub/Kaggle handles) evaluated as a reference ceiling; 2) Lightweight local `musiq.py` approximation (reduced transformer depth/dimensions, 1.41 MB TFLite FP16) probed on 1,024-image subsets.

## 2. Input / Output Contract & Model Artifacts

- **Input Contract**: Multi-scale patch tokens or `224×224` / native-aspect RGB inputs
- **Output Contract**: Scalar quality score
- **Model Files (`models/model_files/` & Releases)**:
  - `musiq_flive_probe1024_fp16.tflite (1.41 MB, SHA256: 1aeaad3d9a1b)`
  - `musiq_koniq_probe1024_fp16.tflite (1.41 MB, SHA256: 8b6d399384f9)`
  - `musiq_spaq_probe1024_fp16.tflite (1.41 MB, SHA256: 97ffd3de9d7e)`

## 3. Benchmark Results

| Model / Variant | Dataset | SRCC | PLCC | Notes |
| :--- | :---: | :---: | :---: | :--- |
| **Official Kaggle MUSIQ (`spaq`)** | SPAQ | **0.9460** | **0.9482** | Heavy multi-scale transformer reference |
| **Official Kaggle MUSIQ (`koniq`)** | KonIQ-10k | **0.9275** | **0.9389** | Heavy multi-scale transformer reference |
| **Official Kaggle MUSIQ (`paq2piq`)** | FLIVE | 0.4815 | 0.5412 | Cross-domain drop on FLIVE |
| **Local MUSIQ Probe1024 (1.41 MB)** | 1,024-row probes | Low / Underfit | - | Rejected for mobile production |

## 4. Key Engineering Notes & 2026 Audit Findings

- **Clear Lineage Separation (2026-07-11 Audit)**: Official Kaggle MUSIQ achieves `0.9460` (SPAQ) and `0.9275` (KonIQ-10k) using full multi-scale hash-grid positional encodings, whereas the 1.41 MB local `musiq_*_probe1024_fp16.tflite` models are tiny reduced-capacity probes that do not reproduce official MUSIQ accuracy.

## 5. Quick Start

```bash
pip install -r requirements.txt
python scripts/smoke_test_kaggle_musiq.py --help
python scripts/predict_musiq.py --help
```

For full documentation, see:
- [`docs/model_card.md`](./docs/model_card.md) — Architecture, tensor contracts, and limitations
- [`docs/benchmark_summary.md`](./docs/benchmark_summary.md) — Detailed metrics and dataset evaluations
- [`docs/reproduction_notes.md`](./docs/reproduction_notes.md) — Environment and reproduction guide
- [`models/download.md`](./models/download.md) — Model binary hashes and download notes

## 6. A-CUT Ecosystem Repositories

| Repository | Dimension | Role / Status | Key Metric |
| :--- | :---: | :--- | :--- |
| [acut-nima-mobile](https://github.com/gwanjongkim/acut-nima-mobile) | Aesthetic (IAA) | **Production Ensemble (0.40)** | AVA SRCC `0.5894`, AUC `0.8018` |
| [acut-rgnet-mobile](https://github.com/gwanjongkim/acut-rgnet-mobile) | Aesthetic (IAA) | **Production Ensemble (0.45)** | AADB SRCC `0.6819` (FP16 `0.6648`) |
| [acut-mobile-alamp](https://github.com/gwanjongkim/acut-mobile-alamp) | Aesthetic (IAA) | **Production Ensemble (0.15)** | AVA Acc `0.7633`, AUC `0.7877` |
| [acut-icaa-color-aesthetics](https://github.com/gwanjongkim/acut-icaa-color-aesthetics) | Color Aesthetics | **Verified TF-Native Port** | ICAA17K Color SRCC `0.8791`, MOS `0.9058` |
| [acut-koniq-flive-technical-iqa](https://github.com/gwanjongkim/acut-koniq-flive-technical-iqa) | Technical (IQA) | **Production Baseline (4/7 + 3/7)** | Official SRCC `0.7168` (`0.7958` recon), `0` Severe FP |
| [acut-technical-iqa](https://github.com/gwanjongkim/acut-technical-iqa) | Technical (IQA) | **Umbrella Benchmark** | 4,967-Image Official Protocol Suite |
| [acut-topiq-mixed112](https://github.com/gwanjongkim/acut-topiq-mixed112) | Technical (IQA) | **Evaluated Candidate** | SPAQ SRCC `0.8990`, KonIQ `0.8630` |
| [acut-topiq-flive-hybrid](https://github.com/gwanjongkim/acut-topiq-flive-hybrid) | Technical (IQA) | **Best Log-Only Shadow (60/40)** | Official SRCC `0.8069`, MAE `5.04` |
| [acut-c6-topiq-koniq](https://github.com/gwanjongkim/acut-c6-topiq-koniq) | Technical (IQA) | **Negative Result (Rejected)** | Official SRCC `0.7314`, MAE `15.39` |
| [acut-mdiqa-benchmark](https://github.com/gwanjongkim/acut-mdiqa-benchmark) | Technical (IQA) | **Teacher Ceiling Reference** | KonIQ SRCC `0.9464`, SPAQ `0.9136` |
| [acut-musiq-probe](https://github.com/gwanjongkim/acut-musiq-probe) | Technical (IQA) | **Reference & Probe Study** | Official SPAQ `0.9460`, KonIQ `0.9275` |
| [acut-student-iqa](https://github.com/gwanjongkim/acut-student-iqa) | Technical (IQA) | **Distillation Study (No-Go)** | 14k Student SRCC `0.7436`, SPAQ `0.8984` |
| [photo_score_project](https://github.com/gwanjongkim/photo_score_project) | Full Monorepo | **Core Research Workspace** | Complete Training, Audit & Pipeline Code |

## 7. References & Citation

- Ke, J., Wang, Q., Wang, Y., Milanfar, P., & Yang, F. (2021). *MUSIQ: Multi-Scale Image Quality Transformer*. IEEE/CVF International Conference on Computer Vision (ICCV), 5148–5157.

```bibtex
@misc{acut_musiq_probe_2026,
  title        = {A-CUT MUSIQ Probe & Reference Benchmark: A-CUT Multi-Scale Image Quality Transformer (MUSIQ) — Official Kaggle Reference Benchmark vs Lightweight Mobile Probes},
  author       = {Kim, Gwanjung},
  year         = {2026},
  howpublished = {\url{https://github.com/gwanjongkim/acut-musiq-probe}}
}
```
