# Reproduction & Execution Notes — A-CUT MUSIQ Probe & Reference Benchmark

## Environment Setup
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

## Available Scripts (`scripts/`)
```bash
python scripts/smoke_test_kaggle_musiq.py --help
python scripts/predict_musiq.py --help
```

## Preprocessing & Parity Verification
- **Input Specification**: Multi-scale patch tokens or `224×224` / native-aspect RGB inputs
- **Output Specification**: Scalar quality score
- Ensure EXIF orientation transposition (`ImageOps.exif_transpose`) is applied prior to resizing so portrait smartphone photos are not evaluated rotated.
