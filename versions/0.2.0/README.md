# Vision Inference Studio 0.2.0

**Package:** [vision-inference-studio_0.2.0_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.2.0/vision-inference-studio_0.2.0_amd64.deb) (88 MB) · **Platform:** Linux x86_64 (tested on Ubuntu 24.04)

The first public test build: a desktop app for running image and video inference workflows locally on an NVIDIA GPU or the CPU.

## Features

- Visual Canvas: connect Image or Video input, Model and Detection Preview nodes, then **Validate** and **Run**.
- Models: YOLO, RF-DETR, DINOv3 and generic ONNX.
- Results in the bottom dock with an Original / Prediction toggle, detection count, timings and GPU memory.
- **Runtime → Status** shows whether CUDA is available.

## Requirements

- 64-bit Linux with a desktop session.
- **Python 3.10 or newer with the `venv` module** (`sudo apt install python3 python3-venv`). Unlike later versions, 0.2.0 uses the system Python.
- Internet on first launch for the private runtime (several GB); about 10 GB of free disk.
- NVIDIA GPU with a recent driver is optional.

## Install

```bash
sha256sum vision-inference-studio_0.2.0_amd64.deb
# 6c6e3ce5bfef852f9721cdfdb01e705b99b7f507a2c1c1875286776c2cdbfd3f
sudo apt install ./vision-inference-studio_0.2.0_amd64.deb
```

`apt` also installs `python3` and `python3-venv` if they are missing. On first launch, click **Install Runtime** (5–20 minutes).

## Notes

- The original 0.2.0 bundle also shipped model weights and a portable archive. **This download is the Debian package only**; add weights with **Upload weights** on the Model node.
- This is an early test build. Use the latest version for real work.
