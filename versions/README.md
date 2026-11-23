# Release notes

One folder per published version, newest first. Each README lists what changed, the requirements, how to install and verify the package, and known limitations.

| Version | Highlights |
|---|---|
| [0.7.9](0.7.9/README.md) | Installs the PyTorch build that matches the computer's GPU and driver: CPU-only (no NVIDIA GPU), CUDA 11.8, 12.1 or 12.8 |
| [0.7.8](0.7.8/README.md) | NVIDIA RTX 50-series (Blackwell) GPU support: installs the CUDA 12.8 PyTorch on these GPUs; Live Output no longer crops portrait images |
| [0.7.7](0.7.7/README.md) | Fix: the private Python runtime installs again (boto3 version conflict in 0.7.5/0.7.6). Models don't run on RTX 50-series GPUs; use 0.7.8 |
| [0.7.6](0.7.6/README.md) | **Private runtime install fails, use 0.7.7.** Training, DeepStream export, optional NVIDIA TAO, cloud storage and datasets, installer reuses an existing Python environment |
| [0.7.4](0.7.4/README.md) | Typed multi-model Canvas, partial runs and caching, Auto Annotation v0.1 |
| [0.5.0](0.5.0/README.md) | RF-DETR feature runtime: feature extraction, difference and heatmap nodes |
| [0.4.0](0.4.0/README.md) | Grounding DINO, SAM, SAM 2.1, SAM 3 and chaiNNer nodes |
| [0.3.0](0.3.0/README.md) | Bundled Python 3.12 and pinned runtime packages |
| [0.2.0](0.2.0/README.md) | First test build: YOLO, RF-DETR, DINOv3 and ONNX on a visual Canvas |

Versions 0.6.x, 0.7.0–0.7.3 and 0.7.5 were not published as separate packages; their changes are included in 0.7.4 and 0.7.6.
