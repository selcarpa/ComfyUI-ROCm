# 构建指南

[English](BUILD_EN.md)

## 默认版本信息

`build.sh` 中预置的默认版本：

| 组件 | 版本 |
|------|------|
| **ComfyUI** | v0.22.0 |
| **ComfyUI-Manager** | 4.2.1（可通过 `COMFYUI_MANAGER_TAG` 指定） |
| **基础镜像** | `rocm/pytorch:rocm7.2.4_ubuntu24.04_py3.12_pytorch_release_2.10.0` |

修改 `build.sh` 中的 `COMFYUI_TAG` 和 `BASE_IMAGE_TAG` 可更换版本。

## 构建镜像

```bash
./build.sh
```

指定版本标签：

```bash
./build.sh v1.0.0
```

构建脚本会自动打两个标签：`selcarpa/comfyui-rocm:latest` 和 `selcarpa/comfyui-rocm:<详细版本>`（含日期、ComfyUI 标签和基础镜像标签）。

可在 `build.sh` 中配置以下参数：
- `COMFYUI_TAG` — ComfyUI Git 标签，用于检出指定版本
- `COMFYUI_MANAGER_TAG` — ComfyUI-Manager Git 标签（或分支），默认 `4.2.1`
- `BASE_IMAGE_TAG` — ROCm PyTorch 基础镜像版本

## 直接使用 docker build

```bash
docker build \
  -f docker/Dockerfile \
  --build-arg COMFYUI_TAG=v0.22.0 \
  --build-arg COMFYUI_MANAGER_TAG=main \
  --build-arg BASE_IMAGE_TAG=rocm7.2.4_ubuntu24.04_py3.12_pytorch_release_2.10.0 \
  -t selcarpa/comfyui-rocm:latest .
```

构建参数说明：
- `COMFYUI_TAG` — ComfyUI Git 标签（如 `v0.22.0`），用于检出指定版本
- `COMFYUI_MANAGER_TAG` — ComfyUI-Manager Git 标签或分支（如 `4.2.1`、`main`），默认 `4.2.1`
- `BASE_IMAGE_TAG` — 基础镜像 `rocm/pytorch` 的版本标签，可从 [Docker Hub](https://hub.docker.com/r/rocm/pytorch/tags) 查找可用版本
