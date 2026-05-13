# llama-cpp-mtp-hip

Arch Linux PKGBUILD for [llama.cpp](https://github.com/ggml-org/llama.cpp) with
[MTP (Multi-Token Prediction)](https://github.com/am17an/llama.cpp/tree/mtp-clean)
speculative decoding support, built with the HIP/ROCm backend for AMD GPUs.

## What is MTP?

Multi-Token Prediction (MTP) is a speculative decoding technique where a draft
model predicts multiple tokens ahead in a single forward pass, and the base
model verifies them in parallel. This can improve inference throughput on
supported hardware.

This package tracks the
[`mtp-clean`](https://github.com/am17an/llama.cpp/tree/mtp-clean) branch by
[am17an](https://github.com/am17an).

## Requirements

- Arch Linux (or derivative)
- ROCm stack: `hip-runtime-amd`, `hipblas`, `rocblas`
- AMD GPU with ROCm support

## Build & Install

```bash
makepkg -si
```

Or install a pre-built package:

```bash
sudo pacman -U llama-cpp-mtp-hip-*.pkg.tar.zst
```

## Source

https://github.com/am17an/llama.cpp/tree/mtp-clean
