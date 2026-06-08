# A-CUT MUSIQ Probe

#### A-CUT Capstone Project — Mobile Image Quality and Aesthetic Assessment

> Local attempt to reproduce or probe MUSIQ.

## Introduction

Repository for probing and benchmarking MUSIQ (Multi-scale Image Quality Transformer) variants. It is not an official full reproduction but a reference benchmark for A-CUT.

- **Role**: Reference/probe benchmark.
- **Task**: Image Quality and Aesthetic Assessment.

## Model / Method

Evaluates official Kaggle MUSIQ checkpoints with custom fallback logic. While demonstrating high performance on SPAQ, it was not selected for mobile production due to integration complexity and specialized requirements.

- **Artifacts**: Inferred from scripts

## Dataset and Benchmark

- Benchmark results are summarized below. See `docs/benchmark_summary.md` for detailed per-dataset analysis.
- Note: Large datasets are excluded due to size/license constraints.

## Model Weights / Artifacts

- Due to size constraints, artifacts larger than 50MB are not included in this repository.
- Recommended hosting: GitHub Releases.
- See `models/download.md`.

## Repository Structure

```
.
├── configs/
├── docs/
├── models/
├── results/
├── scripts/
└── requirements.txt
```

## Requirements

Please refer to `requirements.txt`. Minimal dependencies include `torch`, `tensorflow`, `numpy`, and `pillow`.

## Quick Start

```bash
pip install -r requirements.txt
python scripts/smoke_test_kaggle_musiq.py
```
*(Verify path assumptions in `docs/reproduction_notes.md`)*

## Results

| Dataset | Metric | Value | Evidence Path | Decision |
|---------|--------|-------|---------------|----------|
| SPAQ | Official Kaggle MUSIQ SRCC | 0.9460 | outputs/musiq_kaggle_sanity_fallback_20260601/report.md | Reference |
| KonIQ-10k | Official Kaggle MUSIQ SRCC | 0.9275 | outputs/musiq_kaggle_sanity_fallback_20260601/report.md | Reference |
| FLIVE | Official Kaggle MUSIQ SRCC | 0.4815 | outputs/musiq_kaggle_sanity_fallback_20260601/report.md | Reference |

## Limitations

- Results are based on local reproduction and may not exactly match original papers.
- See `docs/model_card.md` for detailed limitations.

## Citation

```bibtex
@misc{acut_musiq_2026,
  title        = {A-CUT MUSIQ Probe: Mobile Image Quality and Aesthetic Assessment Model},
  author       = {Kim, Gwanjung},
  year         = {2026},
  note         = {Capstone project repository}
}
```
### Original References

- Ke, J., et al. (2021). MUSIQ: Multi-scale Image Quality Transformer. ICCV.

## Related Repositories

- [A-CUT Public Model Repositories](..)
