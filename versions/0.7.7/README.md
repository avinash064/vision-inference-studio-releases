# Vision Inference Studio 0.7.7

**Released:** 2026-11-20 · **Package:** [vision-inference-studio_0.7.7_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.7.7/vision-inference-studio_0.7.7_amd64.deb) (116 MB) · **Platform:** Ubuntu / Debian x86_64

A fix release for 0.7.6. **If you installed 0.7.6, upgrade to 0.7.7.**

## Fixed

- **Installing or updating the private runtime failed** with `ERROR: ResolutionImpossible` and "Cannot install boto3<2 and >=1.35". The app's requirements asked for boto3 1.35 or newer, but its pinned, tested package list uses boto3 1.34.11, so the package installer could not satisfy both.
  - This happened whenever no existing Python environment was reused: in **Install Runtime**, **Update Runtime** and during package installation.
  - 0.7.7 accepts the tested boto3 1.34, and a new automatic check stops the pinned list and the requirements from disagreeing again.

Everything else is the same as [0.7.6](../0.7.6/README.md): training, DeepStream export, optional NVIDIA TAO, cloud storage and datasets, and an installer that reuses a Python environment you already have.

## Install or upgrade

```bash
sha256sum vision-inference-studio_0.7.7_amd64.deb
# 3123f5afaf3cb7a377549645371444cfc8eb6ee9ee556f43bfd1a759dc505f18
sudo apt install ./vision-inference-studio_0.7.7_amd64.deb
```

**If 0.7.6 failed on your computer:** install 0.7.7 the same way. If the installer doesn't finish the runtime, start the app and click **Update Runtime**. Setup continues in the same runtime folder, so packages that were already installed are not downloaded again. Your data and settings are kept.

## Requirements

Same as 0.7.6: 64-bit Ubuntu or Debian with a desktop session, about 15 GB free if the private runtime has to be installed, and optionally an NVIDIA GPU with driver 525 or newer. See the [User Manual](https://github.com/avinash064/vision-inference-studio-releases/blob/main/USER_MANUAL.md#2-requirements).

## Tested

- Backend tests: 317 passed, 9 skipped. Desktop tests: 10 passed. Frontend build: passed.
- A full dry run of both runtime install steps, with the pinned package list, the CUDA 12.1 PyTorch index and prebuilt packages only: resolves with no conflicts.
- Package checks: version 0.7.7 throughout, and no credentials or model weights included.
- The complete private-runtime download on a clean machine was **not tested** in this release; the dry run above covers the step that failed.

## Known limitations

Same as [0.7.6](../0.7.6/README.md#known-limitations).
