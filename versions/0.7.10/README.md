# Vision Inference Studio 0.7.10 — macOS (first macOS build)

**Released:** 2026-11-24 · **Package:** `Vision Inference Studio-darwin-arm64-0.7.10.zip` (152 MB) · **Platform:** macOS (Apple Silicon, arm64)

This is the first macOS build of Vision Inference Studio. It is numbered 0.7.10 rather than 0.7.9 because 0.7.9
was already published for Linux (GPU-driver-matched PyTorch build selection) with a feature set this build does
not include — see [0.7.9](../0.7.9/README.md). Linux and Windows stay on 0.7.9 for now.

## What's included

- Native Electron app for Apple Silicon, with its own relocatable CPython 3.12.15 runtime (the same
  python-build-standalone approach as Linux/Windows) and a managed-runtime installer
  (`packaging/macos/setup-runtime.sh`) that sets up the Python backend on first launch.
- No CUDA on macOS, so PyTorch/torchvision/onnxruntime install as plain CPU/MPS builds automatically — there is
  no GPU-build-matching step to run here (unlike 0.7.9's Linux CUDA selection).
- All the fixes and features from the Linux/Windows 0.6.3 → 0.7.8 line (Cloud Storage, Dataset Registry,
  typed Canvas, training, DeepStream export, Auto Annotation) are present.
- A cross-platform fix also relevant to the next Linux/Windows build: the runtime's pinned `boto3` version was
  below what the storage integration requires, which broke `setup-runtime.sh` on every platform.
- A crash fix: searching the Public Hub (Datasets/Models tab) with Kaggle not configured used to kill the
  entire backend process (`Backend exited code=1`, visible as an Internal Server Error). Unconfigured providers
  now show up as a normal per-provider error instead.

## Install

1. Download `Vision Inference Studio-darwin-arm64-0.7.10.zip` and check it:
   ```bash
   shasum -a 256 "Vision Inference Studio-darwin-arm64-0.7.10.zip"
   # must match: 70e44a60247bd42e3983cd03d7952f1e1a16804efcbf72ce09b4a18d4559cdf4
   ```
2. Unzip it and move `Vision Inference Studio.app` to `/Applications` (or run it in place).
3. **The app is not notarized** (no Apple Developer ID certificate in this build), so Gatekeeper blocks a plain
   double-click the first time. Either right-click the app → **Open** → **Open** in the dialog, or run:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/Vision Inference Studio.app"
   ```
4. On first launch, the app installs its private Python runtime (10–30 minutes, needs internet). Progress shows
   in the window; `runtime-setup.log` (**Help → Open Logs Folder**) has the detail.

## Requirements

Apple Silicon Mac (arm64). No GPU/CUDA requirement — inference runs on CPU (with PyTorch's Apple MPS backend
where supported). About 15 GB free disk space for the private runtime.

## Tested

- `npm run desktop:make` (frontend build, tsc, resource staging, electron-forge package + make): PASS.
- `npm test` (11 desktop tests) and the backend suite (`pytest -m "not integration"`, 293 passed / 4 pre-existing
  unrelated failures needing the `onnx` package, which was never added to any requirements file): PASS.
- Ran the managed-runtime installer end-to-end against the packaged resources (real network installs, no
  mocking): `RUNTIME READY`, every package validated `ok: true`.
- Real load + inference against the installed runtime, one checkpoint per family: **PASS** — `yolo`, `yolo-seg`,
  `rtdetr`, `sam2`, `rfdetr`, `grounding-dino`, `sam` (v1), `paddleocr`, `sam3` (the gated `facebook/sam3`
  checkpoint, point/box-prompted segmentation). **FAIL** — `dinov3` (separately gated HF repo, license not
  accepted by the test account). **Not exercised** — `rtdetrv2` (no scriptable checkpoint URL), `onnx`
  (bring-your-own-weights by design), `vllm` (remote server, nothing to load locally), `tesseract` (no system
  binary on the build machine; works once installed via Homebrew).

## Known limitations

- Unsigned/unnotarized: Gatekeeper requires the manual bypass above.
- Tesseract OCR needs `brew install tesseract`; it is not bundled (unlike the `.deb`'s apt dependency on Linux).
- RF-DETRv2 has no default-download path yet; bring your own `.pth` checkpoint.
- No GPU acceleration profiling has been done on Apple Silicon; inference correctness was verified, not speed.
