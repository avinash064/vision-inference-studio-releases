# Vision Inference Studio 0.7.11

**Released:** 2026-11-25 · **Package:** [vision-inference-studio_0.7.11_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.7.11/vision-inference-studio_0.7.11_amd64.deb) (116 MB) · **Platform:** Ubuntu / Debian x86_64 (NVIDIA GPU or CPU)

A fix release for Linux. **If you use 0.7.4 to 0.7.9 on Linux, upgrade to 0.7.11.**

This release continues the Linux line (0.7.9). It is not a macOS build and doesn't include the macOS changes of [0.7.10](../0.7.10/README.md); macOS users stay on 0.7.10.

## Fixed

### chaiNNer nodes showed as unavailable

**The problem in 0.7.4 to 0.7.9:** almost every chaiNNer image-processing node in the Node Library was greyed out as **Unavailable**. Only 7 of 173 could be used. The reason shown was `No module named 'nodes.properties.outputs'`.

**The cause:** one folder of the bundled chaiNNer code, `nodes/properties/outputs`, was missing from the package. The project's rule for ignoring pipeline output folders (`outputs/`) also matched this folder, so it was never included.

**In 0.7.11:**

- The folder is included, and 162 of 179 chaiNNer nodes are available. This covers all 140 nodes of the standard chaiNNer package.
- The other 17 need engines that the app does not install: `spandrel` (9 PyTorch upscaling nodes), TensorRT (5), NCNN (2) and `facexlib` (1). They still show as unavailable and name the missing engine.
- The package build now stops if any part of the bundled chaiNNer code is missing, so this can't happen again unnoticed.

**macOS 0.7.10** was built from the same chaiNNer code and most likely has the same problem. It was not checked on a Mac, and no fixed macOS build is available yet.

### New model nodes ran on the CPU

**The problem:** a Model node added from the Node Library or the canvas quick picker started with **Device: CPU** and **Precision: fp32**, even on a computer with an NVIDIA GPU. Only **Open in Canvas** and workflows saved with a GPU device used the GPU.

**In 0.7.11:**

- A new model node starts on the computer's first NVIDIA GPU (`cuda:0`) with `fp16`, the same setting **Open in Canvas** uses.
- On a computer without a GPU, it starts on the CPU as before.
- Saved workflows keep the device they were saved with.
- Model nodes you already added on the CPU stay on the CPU. Change **Device** in the Inspector to move them to the GPU.

## Install or upgrade

```bash
sha256sum vision-inference-studio_0.7.11_amd64.deb
# 58f6fdef65814bccbdddf7651bbb911d12ee22aa0644d7f25382ec1c088446b0
sudo apt install ./vision-inference-studio_0.7.11_amd64.deb
```

The Python packages are the same as in 0.7.9:

- **Python environment you chose yourself:** used as-is.
- **Private runtime:** checked and updated in place. Nothing new needs to be downloaded.

Your data and settings are kept.

## Requirements

Same as [0.7.9](../0.7.9/README.md#requirements).

## Tested

- Backend tests: 355 passed, 9 skipped. Desktop tests: 11 passed. Frontend build: passed.
- New tests check:
  - the chaiNNer code loads without a missing module;
  - the package build catches a missing chaiNNer folder.
- **Packaged 0.7.11 app on an RTX 4050** (driver 580):
  - it starts and loads 162 chaiNNer nodes;
  - setup chooses the tested CUDA 12.1 PyTorch build;
  - a saved RF-DETR workflow on `cuda:0` runs on the GPU;
  - a Model node added from the quick picker starts on `cuda:0` with `fp16`.
- Package checks: version 0.7.11 throughout, no macOS files, and no credentials or model weights included.
- Not tested: macOS (this is a Linux package), RTX 50-series GPUs, and computers without an NVIDIA GPU (only the CPU fallback rule itself was checked).

## Known limitations

Same as [0.7.6](../0.7.6/README.md#known-limitations).
