# Vision Inference Studio 0.7.6

**Released:** 2026-11-20 · **Package:** [vision-inference-studio_0.7.6_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.7.6/vision-inference-studio_0.7.6_amd64.deb) (116 MB) · **Platform:** Ubuntu / Debian x86_64

> **Known issue — use [0.7.7](../0.7.7/README.md) instead.** Installing or updating the private Python runtime fails with `ResolutionImpossible` ("Cannot install boto3<2 and >=1.35"). Reusing an existing Python environment works, but if none is found the runtime can't be installed. 0.7.7 fixes this; everything else is the same.

This release adds model training, DeepStream deployment export and optional NVIDIA TAO training, and makes installation reuse a Python environment you already have. It also includes the 0.7.5 changes (cloud storage and datasets), which were not published as a separate package.

## What's new

### Installation reuses your Python environment
- During installation the package searches your computer for a Python environment that already has the required packages: virtualenvs, conda, pyenv, pipenv, `/opt` and the system Python. If it finds one, it uses it as-is, so **no new environment is created and nothing is installed**.
- If none fits, the private runtime is installed **during package installation** instead of on first launch.
- The installer never fails because of this step. If it can't finish, the app offers **Install Runtime** on first launch, which runs the same search first.
- New commands: `vision-inference-studio-setup --discover`, `--use-python <path>` and `--mode auto`.

### Training (new)
- **New Training** and **Training Runs** pages: train or fine-tune Ultralytics YOLO (detection and segmentation), RF-DETR and RT-DETR on a dataset snapshot with COCO labels.
- Live loss, mAP and learning-rate charts, raw logs, saved train/validation splits, best and last checkpoints with checksums.
- **Register Best Model** records full provenance, then lets you Test in Canvas, Fine-tune, or export to DeepStream.

### DeepStream export (new)
- **DeepStream Export** and **Export History** pages: build a validated `nvinfer` bundle from a registered YOLO, RT-DETR or RF-DETR model. The bundle holds ONNX, labels, the nvinfer config, a deepstream-app fragment, metadata, checksums and a README.
- Validated with the ONNX checker, ONNX Runtime and a comparison against the original model. Save locally or upload to a storage connection.

### NVIDIA TAO (new, optional)
- Train TAO 7.3 DINO and RT-DETR from the same Training page, using pinned TAO containers in local Docker.
- **Settings → NVIDIA TAO** runs a preflight of Docker, the NVIDIA runtime, the GPU, the driver against the container's CUDA, disk space and GPU memory for each model.
- Your NGC key is read from `.env` and never stored in the app.

### Cloud storage and datasets (from 0.7.5)
- **Storage** page: Local, Google Cloud Storage and AWS S3 connections with browsing, preview, download and upload. Credentials are referenced as `env:NAME`, never stored.
- **Datasets:** register a `manifest.jsonl`, validate it FAST or DEEP, search and preview items, and pin immutable **snapshots**.
- Snapshots work as the Canvas image input, as an Auto Annotation source and as training data.

### Fixes and improvements
- The Live Output panel can be enlarged, minimized and drag-resized again, and remembers its size.
- The panel's compile check and its result summaries for masks, OCR text, features and heatmaps are back.
- Uploads to cloud storage keep the right content type, so image previews work.

## Requirements

- 64-bit Ubuntu or Debian with a desktop session.
- About 15 GB of free disk if the private runtime has to be installed; none extra if an existing environment is reused.
- NVIDIA GPU with driver 525 or newer is optional; without one the app uses the CPU.
- For TAO only: Docker, the NVIDIA Container Toolkit, an NGC key, an 8–16 GB GPU and about 45 GB of disk.

## Install or upgrade

```bash
sha256sum vision-inference-studio_0.7.6_amd64.deb
# 6bf7a55a4abf08b5df867061b533ef2c32d4ef0eab61c73a20a8be16c6f2038c
sudo apt install ./vision-inference-studio_0.7.6_amd64.deb
```

Upgrading from any earlier version keeps your weights, workflows, recipes, datasets and settings. See the [User Manual](../../USER_MANUAL.md#3-install-upgrade-and-the-python-runtime) for details of the runtime setup.

## Tested

- Backend tests: 311 passed, 9 skipped (tests needing real models are skipped by default). Desktop tests: 10 passed. Runtime-reuse checks: 5 passed. Frontend build: passed.
- Real training: YOLO for 60 epochs (mAP50 0.400) and RF-DETR for 2 epochs (mAP50 0.591). Both were registered and run in Canvas.
- Both DeepStream bundles ran in DeepStream 8.0: 601 frames processed, exit code 0.
- Installer runtime reuse: an existing environment was found and selected without installing anything (about 7 seconds).

## Known limitations

- **Private runtime install fails** (boto3 version conflict). Fixed in [0.7.7](../0.7.7/README.md).
- **TAO:** only the preflight was run on real hardware. Real TAO training was **not tested** because the test machine lacked disk space and GPU memory.
- **Installer:** the fallback that installs the full private runtime during `apt install` was **not tested** end to end on a clean machine.
- **Real S3:** dataset acceptance was **not tested**; Google Cloud Storage was.
- No model weights are included; add your own.
