# Vision Inference Studio 0.7.8

**Released:** 2026-11-23 · **Package:** [vision-inference-studio_0.7.8_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.7.8/vision-inference-studio_0.7.8_amd64.deb) (116 MB) · **Platform:** Ubuntu / Debian x86_64

Adds support for NVIDIA Blackwell GPUs, including every GeForce RTX 50-series desktop and laptop GPU. **If you have one of these GPUs, upgrade to 0.7.8.**

## New: NVIDIA RTX 50-series (Blackwell) GPUs

**The problem in 0.7.7 and earlier:** workflows did not run on these GPUs. Examples: the RTX 5050, 5060, 5070, 5080 and 5090 desktop and laptop GPUs, and RTX PRO Blackwell. **Runtime → Status** said `CUDA READY`, but every model failed with `CUDA error: no kernel image is available for the execution device`.

**The cause:** the app installed a PyTorch build (2.5.1 for CUDA 12.1) that has no code for these GPUs. Their compute capability is 10.0 or newer (12.0 for the RTX 50-series), and that build stops at 9.0.

**What 0.7.8 changes:**

- **The right PyTorch for your GPU.** Setup reads your GPU's compute capability from `nvidia-smi`.
  - On Blackwell GPUs it installs PyTorch 2.7.1 built for CUDA 12.8. This needs **NVIDIA driver 570 or newer**.
  - Older GPUs keep the tested PyTorch 2.5.1 build, so nothing changes for them.
- **Existing private runtimes are updated.** A private runtime built for another GPU generation is updated the next time setup runs.
- **Environments without GPU code are skipped.** When the installer searches for an existing Python environment, it no longer picks one whose PyTorch has no code for your GPU.
- **A clear message instead of the CUDA error.**
  - **Runtime → Status** shows `GPU NOT SUPPORTED BY PYTORCH` with the reason.
  - A model set to the GPU stops on load with that explanation.

## Fixed

- **Live Output cropped tall (portrait) images.** They now fit the panel completely.

## Install or upgrade

```bash
sha256sum vision-inference-studio_0.7.8_amd64.deb
# 5044e43e77b156fc97258ceaff74cec11f75a8a8faeb31fe393ef9fa660c67bd
sudo apt install ./vision-inference-studio_0.7.8_amd64.deb
```

**On an RTX 50-series computer:**

1. Check the driver first with `nvidia-smi`. The **Driver Version** must be 570 or newer; update it if not.
2. Install 0.7.8. If the installer reports that the runtime needs updating, start the app and click **Update Runtime**. This downloads the CUDA 12.8 PyTorch and its CUDA libraries, a few GB.
3. Open **Runtime → Status**. It should show `CUDA READY`.

**If you chose your own Python environment** (with `vision-inference-studio-setup --use-python`), setup never changes it. If it has the older PyTorch, upgrade it yourself:

```bash
/path/to/your/python -m pip install --upgrade torch==2.7.1 torchvision==0.22.1 --index-url https://download.pytorch.org/whl/cu128
```

To force a PyTorch build, set `VIS_TORCH_BUILD=cu121` or `VIS_TORCH_BUILD=cu128` when you run `vision-inference-studio-setup`.

## Requirements

Same as 0.7.7: 64-bit Ubuntu or Debian with a desktop session, and about 15 GB free if the private runtime has to be installed. An NVIDIA GPU is optional:

- **RTX 50-series and other Blackwell GPUs:** driver 570 or newer.
- **Other NVIDIA GPUs:** driver 525 or newer.

See the [User Manual](https://github.com/avinash064/vision-inference-studio-releases/blob/main/USER_MANUAL.md#2-requirements).

## Tested

- Backend tests: 335 passed, 9 skipped. Desktop tests: 10 passed. Frontend build: passed.
- New tests cover the GPU code check, choosing the PyTorch build, and the CUDA 12.8 pinned package list.
- A dry run of both runtime install steps with the CUDA 12.8 package list resolves with no conflicts: PyTorch 2.7.1+cu128, torchvision 0.22.1+cu128 and the matching CUDA 12.8 libraries.
- On an RTX 4050 (compute capability 8.9): the GPU is reported as supported, and the packaged 0.7.8 app starts and runs its backend.
- Package checks: version 0.7.8 throughout, the new package list is included, and no credentials or model weights are included.
- **Not tested on an RTX 50-series GPU.** No Blackwell GPU was available for this release, so the following are not yet confirmed:
  - running models with the CUDA 12.8 PyTorch on such a GPU;
  - ONNX models on such a GPU;
  - the complete private-runtime download on a clean machine.

  Please [report](https://github.com/avinash064/vision-inference-studio-releases/issues) how it works on your RTX 50-series GPU, with the output of `nvidia-smi`.

## Known limitations

Same as [0.7.6](../0.7.6/README.md#known-limitations).
