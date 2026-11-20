# Vision Inference Studio 0.4.0

**Package:** [vision-inference-studio_0.4.0_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.4.0/vision-inference-studio_0.4.0_amd64.deb) (177 MB) · **Platform:** Linux x86_64 (Ubuntu / Debian)

This release adds prompt-based detection and segmentation models, plus the chaiNNer image-processing nodes.

## What's new

- **Grounding DINO** (Swin-T, official IDEA-Research): finds objects you name in text.
- **SAM (ViT-B)** and **SAM 2.1 (Hiera B+)**: segment the object you point at, by point or box.
- **SAM 3**: segments every instance of a named concept, or one object by point or box.
- **chaiNNer nodes** (162) in the node library.
- Grounding DINO and the CLIP tokenizer for SAM 3 install from files included in the app; no compiler is needed.

## Requirements

- 64-bit Linux with a desktop session and glibc 2.28 or newer (Ubuntu 20.04+, Debian 11+, Fedora 29+).
- About 15 GB of free disk for the runtime; 16 GB of RAM recommended (SAM 3 briefly needs 6–7 GB to load).
- NVIDIA GPU with driver 525 or newer is optional. SAM 3 needs about 4 GB of GPU memory; the other models need 1–2.5 GB.
- Python is not required.

## Install

```bash
sha256sum vision-inference-studio_0.4.0_amd64.deb
# f86823113d11731c5593554b5259e162b7b045135aa279f12d546246b25ebb25
sudo apt install ./vision-inference-studio_0.4.0_amd64.deb
```

On first launch, click **Install Runtime** (5–20 minutes). Upgrading from 0.2.0 or 0.3.0 shows **Runtime update required**; click **Update Runtime**.

## Quick test

- **Grounding DINO:** enter text such as `person, car`, and connect a **Detection Preview**.
- **SAM 3:** enter text such as `person`, or a point `x,y` or a box `x1,y1,x2,y2`, and connect a **Segmentation Preview**.
- SAM 3 takes about 10 seconds to load. Switching between its text and point/box modes reloads it.

## Notes

- The original 0.4.0 bundle also shipped model weights. **This download is the application package only**; add weights with **Upload weights** on the Model node.
- For RF-DETR large, a "deprecated model configuration" warning in the logs is normal.
