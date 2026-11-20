# Vision Inference Studio 0.7.4

**Package:** [vision-inference-studio_0.7.4_amd64.deb](https://github.com/avinash064/vision-inference-studio-releases/releases/download/v0.7.4/vision-inference-studio_0.7.4_amd64.deb) (116 MB) · **Platform:** Ubuntu / Debian x86_64

Canvas becomes a typed, multi-model workflow runtime, and the first Auto Annotation module is built in. It also includes the 0.6.x and 0.7.0–0.7.3 changes, which were not published as separate packages.

## What's new

- **Typed workflows:** named, typed ports, stable node IDs, automatic migration of older workflows, and clear validation messages that name the node and the problem.
- **Model-to-model pipelines:** detector → classifier, detector → SAM, fan-out and fan-in.
- **Partial runs:** Run Node, Run Until and Run From, with per-node status (`NOT_RUN`, `RUNNING`, `COMPLETED`, `FAILED`, `CACHED`), timing, inputs, outputs and errors.
- **Caching:** results are cached by settings and inputs; changing one node reruns only what depends on it.
- **Scheduling:** CPU-safe nodes run in parallel; GPU work is scheduled with memory awareness.
- **Recipes** freeze the whole graph and pin every model.
- **Auto Annotation v0.1:** run a recipe over an image folder or video with deterministic frame sampling and retention rules. Runs are durable and resumable, can be reviewed visually, and produce validated canonical, COCO and YOLO packages.
- **More models (from 0.6.x):** RF-DETR architecture and patch-size selection, official RT-DETRv2, YOLO segmentation, PaddleOCR and Tesseract OCR, remote vLLM vision models, and imported chaiNNer nodes.
- Runtime diagnostics in the header, and a more reliable desktop app.

## Requirements

- 64-bit Ubuntu or Debian with a desktop session; about 15 GB of free disk for the runtime.
- NVIDIA GPU with driver 525 or newer is optional.

## Install

```bash
sha256sum vision-inference-studio_0.7.4_amd64.deb
# 4a96c0546cd8183a613058a2c07b070c42e84b53babecb61515d9ee2360c1b4c
sudo apt install ./vision-inference-studio_0.7.4_amd64.deb
```

On first launch, click **Install Runtime**, which installs a private runtime in 10–30 minutes. Existing data is kept on upgrade.

## Tested

- Backend: 190 passed, 9 skipped. Frontend build and desktop tests (10): passed.
- Installed app startup and authenticated health check: passed.

## Known limitations

- Auto Annotation v0.1 accepts local image folders and videos only; cloud datasets arrived in 0.7.6.
- No model weights are included.
