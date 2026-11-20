# Vision Inference Studio 0.3.0

**Package:** [vision-inference-studio_0.3.0_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.3.0/vision-inference-studio_0.3.0_amd64.deb) (168 MB) · **Platform:** Linux x86_64 (Ubuntu / Debian)

This release removes the need for system Python and pins every runtime package to tested versions.

## What's new

- **No system Python needed.** The app includes its own Python 3.12.15, so it behaves the same whether the machine has Python 3.10, 3.14 or none at all.
- **Pinned packages.** The inference runtime installs exact package versions from a lock file, tested with real YOLO and RF-DETR inference.

## Requirements

- 64-bit Linux with a desktop session and glibc 2.28 or newer (Ubuntu 20.04+, Debian 11+, Fedora 29+).
- Internet on first launch, to download the inference runtime (about 4 GB).
- About 15 GB of free disk (the installed runtime is about 10 GB).
- NVIDIA GPU with driver 525 or newer is optional.

## Install

```bash
sha256sum vision-inference-studio_0.3.0_amd64.deb
# 6e3b03062c22071ef96fe57c44b86fdf8eef932a3df88c439ee52c97b02f624c
sudo apt install ./vision-inference-studio_0.3.0_amd64.deb
```

On first launch, click **Install Runtime** (5–20 minutes). Supported models: YOLO, RF-DETR, DINOv3 and ONNX.

## Notes

- The original 0.3.0 bundle also shipped model weights and a portable archive. **This download is the Debian package only**; add weights with **Upload weights** on the Model node.
