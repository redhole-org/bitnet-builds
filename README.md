# BitNet Builds

Pre-built BitNet inference binaries for Rednode.

Builds Microsoft's [BitNet](https://github.com/microsoft/BitNet) `llama-server` (renamed `bitnet-server`) for all platforms via GitHub Actions CI.

## Platforms

| Platform | Runner | Archive |
|----------|--------|---------|
| macOS ARM64 (Apple Silicon) | `macos-14` | `bitnet-macos-arm64.tar.gz` |
| Linux x86_64 | `ubuntu-24.04` | `bitnet-linux-x64.tar.gz` |
| Windows x64 | `windows-2022` | `bitnet-windows-x64.zip` |

## Binaries

Each release contains:
- `bitnet-server` — HTTP server with OpenAI-compatible API (`/v1/chat/completions`)
- `bitnet-cli` — CLI inference tool

## Usage

### Trigger a build

**Manual dispatch:** Actions → Build BitNet → Run workflow (optionally specify a BitNet repo ref)

**Tagged release:** Push a version tag to auto-build and publish release assets:
```bash
git tag v1.0.0
git push origin v1.0.0
```

### Run the server

```bash
./bitnet-server \
  -m /path/to/ggml-model-i2_s.gguf \
  --host 127.0.0.1 \
  --port 8080 \
  -t 4 -c 2048 -ngl 0 -cb
```

### Recommended model

[BitNet-b1.58-2B-4T](https://huggingface.co/microsoft/BitNet-b1.58-2B-4T) — 2.4B params, 1.19 GB GGUF, ~0.4 GB RAM for weights.

Pre-converted GGUF available at [microsoft/BitNet-b1.58-2B-4T-gguf](https://huggingface.co/microsoft/BitNet-b1.58-2B-4T-gguf).

## Kernel configuration

Builds are optimized for BitNet-b1.58-2B-4T model dimensions. The kernel codegen parameters are defined as env vars in the workflow and can be adjusted for other models.

## License

BitNet is MIT licensed by Microsoft. This repo only contains build automation.
