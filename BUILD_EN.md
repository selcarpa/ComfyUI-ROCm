# Build Guide

[中文](BUILD.md)

## Default Version Info

Default versions configured in `build.sh`:

| Component | Version |
|-----------|---------|
| **ComfyUI** | v0.22.0 |
| **ComfyUI-Manager** | 4.2.1 (configurable via `COMFYUI_MANAGER_TAG`) |
| **Base Image** | `rocm/pytorch:rocm7.2.4_ubuntu24.04_py3.12_pytorch_release_2.10.0` |

Edit `COMFYUI_TAG`, `COMFYUI_MANAGER_TAG`, and `BASE_IMAGE_TAG` in `build.sh` to change versions.

## Build Image

```bash
./build.sh
```

Or with a version tag:

```bash
./build.sh v1.0.0
```

The script tags the image as both `selcarpa/comfyui-rocm:latest` and `selcarpa/comfyui-rocm:<detailed-version>` (includes date, ComfyUI tag and base image tag).

The following variables can be configured in `build.sh`:
- `COMFYUI_TAG` — ComfyUI Git tag to checkout
- `COMFYUI_MANAGER_TAG` — ComfyUI-Manager Git tag or branch (default: `4.2.1`)
- `BASE_IMAGE_TAG` — ROCm PyTorch base image version

## Using docker build directly

```bash
docker build \
  -f docker/Dockerfile \
  --build-arg COMFYUI_TAG=v0.22.0 \
  --build-arg COMFYUI_MANAGER_TAG=main \
  --build-arg BASE_IMAGE_TAG=rocm7.2.4_ubuntu24.04_py3.12_pytorch_release_2.10.0 \
  -t selcarpa/comfyui-rocm:latest .
```

Build arguments:
- `COMFYUI_TAG` — ComfyUI Git tag (e.g. `v0.22.0`), checked out at build time
- `COMFYUI_MANAGER_TAG` — ComfyUI-Manager Git tag or branch (e.g. `4.2.1`, `main`), defaults to `4.2.1`
- `BASE_IMAGE_TAG` — Version tag for the base image `rocm/pytorch`. Available tags can be found on [Docker Hub](https://hub.docker.com/r/rocm/pytorch/tags).
