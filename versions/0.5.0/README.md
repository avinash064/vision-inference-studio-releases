# Vision Inference Studio 0.5.0

**Package:** [vision-inference-studio_0.5.0_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.5.0/vision-inference-studio_0.5.0_amd64.deb) (177 MB) · **Platform:** Linux x86_64 (Ubuntu / Debian)

This release adds an RF-DETR **feature runtime**: extract, compare and visualise internal feature maps, for example to detect changes between a reference image and a current image.

## What's new

- **Feature providers:**
  - RF-DETR v2.2 (Large, 560 px): fine 80×80 and coarse 20×20 feature levels.
  - RF-DETR Architecture B (Seg Large, 504 px): a 42×42 backbone level from a single forward pass.
  - DINOv3 is unchanged.
- **New nodes:**
  - **Feature Extract**, **Feature Normalize**, **Feature Difference** (raw, absolute, L2 or cosine; it refuses to compare mismatched feature spaces and never resizes silently).
  - **RF-DETR Activation XOR** and **Mahalanobis Feature Difference**, which uses a frozen geometry.
  - **Heatmap** and **Feature Preview**.
- **Feature store:** features stay on the GPU between nodes, with explicit size limits. Nothing is evicted silently; when a limit is reached you get a clear error.
- One model load serves both the reference and current images.

## Requirements

- 64-bit Linux with a desktop session and glibc 2.28 or newer (Ubuntu 20.04+, Debian 11+).
- About 15 GB of free disk for the runtime. NVIDIA GPU with driver 525 or newer is optional.
- Python is not required; the app includes Python 3.12.

## Install

```bash
sha256sum vision-inference-studio_0.5.0_amd64.deb
# e8ac0ed9270b740016cd33916f19928537ae005409a3b49dda57c6ce59c67136
sudo apt install ./vision-inference-studio_0.5.0_amd64.deb
```

On first launch, click **Install Runtime** (5–20 minutes). Upgrading from 0.4.0 shows **Runtime update required**; click **Update Runtime**.

## Notes

- No model weights are included. Add your own RF-DETR or DINOv3 checkpoints with **Upload weights**.
