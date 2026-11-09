# Model Card — A-CUT MUSIQ Probe & Reference Benchmark

## Model Details
- **Model Name**: A-CUT MUSIQ Probe & Reference Benchmark (`acut-musiq-probe`)
- **Developer**: Gwanjung Kim (A-CUT Mobile Photo Evaluation & Curation Capstone)
- **Architecture**: 1) Official Google Research MUSIQ (`spaq`, `koniq`, `paq2piq` TF-Hub/Kaggle handles) evaluated as a reference ceiling; 2) Lightweight local `musiq.py` approximation (reduced transformer depth/dimensions, 1.41 MB TFLite FP16) probed on 1,024-image subsets.
- **Deployment Role**: Reference Benchmark & Lightweight Mobile Probe Study (Negative Result for 1,024-row local probes)

## Tensor Input / Output Contract
- **Input Contract**: Multi-scale patch tokens or `224×224` / native-aspect RGB inputs
- **Output Contract**: Scalar quality score
- **Included Model Artifacts**:
  - `musiq_flive_probe1024_fp16.tflite (1.41 MB, SHA256: 1aeaad3d9a1b)`
  - `musiq_koniq_probe1024_fp16.tflite (1.41 MB, SHA256: 8b6d399384f9)`
  - `musiq_spaq_probe1024_fp16.tflite (1.41 MB, SHA256: 97ffd3de9d7e)`

## Intended Use
- Designed for on-device or offline photo quality and aesthetics evaluation within the A-CUT smartphone photo selection pipeline.
- Not intended as an uncalibrated standalone medical, forensic, or safety-critical classifier.

## Limitations & Audit Qualifications
- **Clear Lineage Separation (2026-07-11 Audit)**: Official Kaggle MUSIQ achieves `0.9460` (SPAQ) and `0.9275` (KonIQ-10k) using full multi-scale hash-grid positional encodings, whereas the 1.41 MB local `musiq_*_probe1024_fp16.tflite` models are tiny reduced-capacity probes that do not reproduce official MUSIQ accuracy.
