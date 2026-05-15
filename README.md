# llama-cpp-mtp-hip

Arch Linux PKGBUILD for [llama.cpp](https://github.com/ggml-org/llama.cpp) with
draft-mtp speculative decoding, using the HIP/ROCm backend for AMD GPUs. This
package builds the `mtp-clean` branch by [am17an](https://github.com/am17an),
which provides MTP and ngram-mod speculative decoding for ROCm.

## What is MTP?

Multi-Token Prediction (MTP) lets a draft model guess several tokens at once and
the base model verify them in parallel. On the right hardware it speeds up
inference significantly.

## Speculative Decoding Usage

The built binaries support multiple speculative decoding types via `--spec-type`:

```
--spec-type none,draft-simple,draft-eagle3,draft-mtp,ngram-simple,ngram-map-k,ngram-map-k4v,ngram-mod,ngram-cache
```

- **draft-mtp** — MTP-style draft model (the primary feature of this package)
- **ngram-mod** — improved ngram-based speculative decoding with configurable parameters
- **ngram-simple** — classic ngram speculative decoding
- **draft-simple** — simple n-gram draft model
- **draft-eagle3** — Eagle-3 style draft model
- **ngram-map-k / ngram-map-k4v / ngram-cache** — variant ngram strategies

### Multi-type (parallel) drafting

You can chain multiple speculative types for parallel drafting:

```bash
llama-cli -m model.gguf --spec-type ngram-mod,draft-mtp -p "Hello"
```

This enables both ngram-mod and draft-mtp speculative decoding simultaneously.

### Additional speculative decoding options

```bash
# Enable default speculative config
--spec-default

# ngram-mod parameters
--spec-ngram-mod-n-min N      # minimum ngram tokens (default: 48)
--spec-ngram-mod-n-max N      # maximum ngram tokens (default: 64)
--spec-ngram-mod-n-match N    # ngram-mod lookup length (default: 24)

# Draft model parameters
--spec-draft-n-max N          # max draft tokens to generate
```

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
