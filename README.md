# llama-cpp-mtp-hip

Arch Linux PKGBUILD for [llama.cpp](https://github.com/ggml-org/llama.cpp) with
MTP speculative decoding, using the HIP/ROCm backend for AMD GPUs. This package
was created to support the new generation of MTP-capable models as introduced in
[llama.cpp PR #22673](https://github.com/ggml-org/llama.cpp/pull/22673).

## What is MTP?

Multi-Token Prediction (MTP) lets a draft model guess several tokens at once and
the base model verify them in parallel. On the right hardware it speeds up
inference significantly. Upstream support was added in
[PR #22673](https://github.com/ggml-org/llama.cpp/pull/22673). This package
builds the `mtp-clean` branch by [am17an](https://github.com/am17an), which
provides the complete MTP speculative decoding pipeline for ROCm.

## Requirements

- Arch Linux (or a derivative)
- ROCm packages: `hip-runtime-amd`, `hipblas`, `rocblas`
- An AMD GPU with ROCm support

## Build

```bash
makepkg -si
```

## License

The PKGBUILD and supporting files in this repository are GPLv3. The upstream
llama.cpp source it builds is MIT — see
[the llama.cpp repository](https://github.com/ggml-org/llama.cpp) for details.
