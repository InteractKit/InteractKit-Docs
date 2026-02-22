# Installation

## Prerequisites

- Go 1.24+
- CGO dependencies: `libsamplerate`, `libopus`, `libsoxr`, `librnnoise`
- [ONNX Runtime](https://github.com/microsoft/onnxruntime/releases) shared library
- [Silero VAD ONNX model](https://github.com/snakers4/silero-vad)

## Install CGO Dependencies

### Ubuntu / Debian

```bash
sudo apt-get install libsamplerate0-dev libopus-dev libsoxr-dev
```

### macOS

```bash
brew install libsamplerate opus libsoxr
```

## Build

```bash
CGO_ENABLED=1 go build -o interactkit .
```
