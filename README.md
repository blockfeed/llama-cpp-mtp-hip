# llama-cpp-mtp-hip

Arch Linux PKGBUILD for [llama.cpp](https://github.com/ggml-org/llama.cpp) with
MTP speculative decoding, using the HIP/ROCm backend for AMD GPUs.

## What is MTP?

Multi-Token Prediction lets a draft model guess several tokens at once and the
base model verify them in parallel. On the right hardware it speeds up inference.
This package builds the `mtp-clean` branch by [am17an](https://github.com/am17an).

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
