# Vision Inference Studio 0.7.9

**Released:** 2026-11-23 · **Package:** [vision-inference-studio_0.7.9_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.7.9/vision-inference-studio_0.7.9_amd64.deb) (116 MB) · **Platform:** Ubuntu / Debian x86_64

The installer now installs the PyTorch build that matches **the GPU and NVIDIA driver of the computer it is installed on**.

## New: PyTorch matched to your GPU

While the package installs, setup reads two things from `nvidia-smi`: your GPU (the newest one, if there are several) and your NVIDIA driver version. It then installs one of these PyTorch builds:

| Your computer | PyTorch installed |
|---|---|
| No NVIDIA GPU, or the NVIDIA driver isn't installed | 2.5.1, CPU-only. About 3 GB less to download, because it needs no CUDA libraries. |
| NVIDIA GPU older than compute capability 5.0 (for example Tesla K80), or a driver older than 450 | 2.5.1, CPU-only. PyTorch can't use these GPUs. |
| NVIDIA driver 450–524 | 2.5.1 for CUDA 11.8 |
| NVIDIA driver 525 or newer, GPUs up to the RTX 40-series, L4 and H100 | 2.5.1 for CUDA 12.1, the tested build (same as before) |
| RTX 50-series and other Blackwell GPUs | 2.7.1 for CUDA 12.8, which needs driver 570 or newer (as in 0.7.8) |

All other packages stay at the same tested versions; only the PyTorch-related packages change.

**See what was chosen:**

- Run `vision-inference-studio-setup --print-torch-build`. It prints the build, the reason and your GPU, and installs nothing.
- `runtime-setup.log` (**Help → Open Logs Folder**) records the same.

**Changed your driver or GPU?** Click **Runtime → Repair Runtime**. Setup rebuilds the private runtime with the matching PyTorch and removes the libraries of the old one.

- On a computer that got the CPU build because the driver was missing, **Runtime → Status** tells you to do this after you install the driver.
- To force a build, run setup with `VIS_TORCH_BUILD` set to `cpu`, `cu118`, `cu121` or `cu128`.

## Install or upgrade

```bash
sha256sum vision-inference-studio_0.7.9_amd64.deb
# 64ac38f9e87326250c071f5830d0e4531549fc22cf8dce755a7269c41698cb4b
sudo apt install ./vision-inference-studio_0.7.9_amd64.deb
```

**What happens to your existing setup:**

- **Python environment you chose yourself:** setup never changes it.
- **Private runtime with a different build:** it is rebuilt during installation. This is the case on a computer without an NVIDIA GPU, which had the CUDA 12.1 build before 0.7.9. The rebuild downloads the packages again (10–30 minutes). Your data and settings are kept.
- **Private runtime that already has the matching build:** it is updated in place.

## Requirements

Same as 0.7.8: 64-bit Ubuntu or Debian with a desktop session, and about 15 GB free if the private runtime has to be installed. An NVIDIA GPU is optional; see the table above for which driver gives which build.

## Tested

- Backend tests: 353 passed, 9 skipped. Desktop tests: 10 passed. Frontend build: passed.
- **Build choice on 12 simulated computers:** no driver, no GPU, RTX 4050, RTX 5050, RTX 5090 with an old driver, B200, Tesla T4 with driver 515, GTX 1080 with drivers 470 and 440, Tesla K80, a mixed RTX A2000 and RTX 5070 system, and an old `nvidia-smi`. The Linux and Windows installers choose the same build on each.
- **On this computer** (RTX 4050, driver 580): the packaged installer chooses the tested CUDA 12.1 build, and the packaged app starts and runs its backend.
- **Dry runs:** the CPU build resolves to 171 packages with no CUDA libraries, and the CUDA 12.8 build resolved in 0.7.8.
- **Package checks:** version 0.7.9 throughout, every pinned package list is included, and no credentials or model weights are included.

**Not tested:**

- A real install of the CUDA 11.8 build. Its pins come from that PyTorch build's own dependency list, but no dry run was done because it downloads about 1 GB.
- Real installs on computers other than the RTX 4050.
- The Windows installer, beyond the shared tests.

## Known limitations

Same as [0.7.6](../0.7.6/README.md#known-limitations). RTX 50-series GPUs have not been tested on real hardware yet; see [0.7.8](../0.7.8/README.md#tested).
