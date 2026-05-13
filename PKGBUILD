# Maintainer: blockfeed <blockfeed@users.noreply.github.com>
pkgname=llama-cpp-mtp-hip
_pkgver=1.0.0
pkgver=1.0.0.mtp.r0
pkgrel=1
epoch=
pkgdesc='llama.cpp with MTP speculative decoding support (HIP/ROCm backend, am17an/mtp-clean branch)'
url='https://github.com/am17an/llama.cpp/tree/mtp-clean'
license=('MIT')
arch=('x86_64')
depends=(curl hip-runtime-amd hipblas openmp rocblas)
makedepends=(cmake git python clang make)
optdepends=(
  'python: for convert_llama_ggml_to_gguf.py, convert_lora_to_gguf.py scripts'
)
provides=('llama.cpp' 'llama-cli' 'llama-server')
conflicts=('llama-cpp-hip' 'llama.cpp-git')
source=("git+https://github.com/am17an/llama.cpp.git#branch=mtp-clean")
sha256sums=('SKIP')

prepare() {
  # The source git+ protocol may produce a bare repo; ensure a working tree exists
  if [ ! -f "llama.cpp/CMakeLists.txt" ]; then
    rm -rf llama.cpp
    git clone --branch mtp-clean --depth 1 https://github.com/am17an/llama.cpp.git llama.cpp
  fi
  if [ -d "llama.cpp/build" ]; then
    rm -rf llama.cpp/build
  fi
}

build() {
  cd llama.cpp
  cmake -B build \
    -DBUILD_SHARED_LIBS=OFF \
    -DGGML_HIP=ON \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX="${pkgdir}/usr"
  cmake --build build -j$(nproc) --target llama-cli llama-server
}

package() {
  cd llama.cpp

  # Core binaries
  install -Dm755 build/bin/llama-cli        "${pkgdir}/usr/bin/llama-cli"
  install -Dm755 build/bin/llama-server     "${pkgdir}/usr/bin/llama-server"

  # Additional CLI tools
  local targets=(
    llama-batched llama-batched-bench llama-bench llama-completion
    llama-cvector-generator llama-debug llama-embedding
    llama-eval-callback llama-finetune llama-gguf-info
    llama-gritlm-stats llama-id2tok llama-imatrix
    llama-infill llama-jnaid-embed llama-perf
    llama-quantize llama-retrieval llama-samplers-demo
    llama-speculative llama-split llama-tokenize
  )

  for t in "${targets[@]}"; do
    if [ -f "build/bin/${t}" ]; then
      install -Dm755 "build/bin/${t}" "${pkgdir}/usr/bin/${t}"
    fi
  done

  # Helper script
  if [ -f "examples/convert-hf-to-gguf/convert-hf-to-gguf.py" ]; then
    cp examples/convert-hf-to-gguf/convert-hf-to-gguf.py \
      "${pkgdir}/usr/bin/convert_hf_to_gguf.py"
  elif [ -f "models/convert-hf-to-gguf.py" ]; then
    cp models/convert-hf-to-gguf.py "${pkgdir}/usr/bin/convert_hf_to_gguf.py"
  fi

  # Documentation
  install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}/"
}
