# SageAttention2 Colab Wheels

Prebuilt wheels of **SageAttention 2.1.2** for Google Colab, compiled for **NVIDIA GPUs with Compute Capability 7.5 (SM75)**, including the free **Tesla T4** available in Google Colab.

## Repository structure

- **[`legacy_wheels/`](legacy_wheels/README.md)** — built from [Ph0rk0z/SageAttention2](https://github.com/Ph0rk0z/SageAttention2). Confirmed broken on **Krea 2** and **Flux-family DiT models**; confirmed working on **MiniMax H3**.
- **[`optimized_wheels/`](optimized_wheels/README.md)** — built from an updated fork, [1506086927/SageAttention2_Optimized_Test](https://github.com/1506086927/SageAttention2_Optimized_Test). Does not have the Krea 2 / Flux-family DiT issues seen in `legacy_wheels`.

## Compatibility

These wheels are intended for:

- Linux
- Google Colab
- NVIDIA Tesla T4 (SM75)
- Other NVIDIA GPUs with Compute Capability 7.5 (SM75)

## Available builds

| Build | PyTorch | CUDA | Python |
|-------|---------|------|--------|
| **Recommended** | 2.11.0 | 13.0 | cp312, cp313 |
| Old | 2.11.0 | 12.8 | cp312, cp313 |
| 2.13.0+cu130 | 2.13.0 | 13.0 | cp312, cp313 |
| **Latest** | 2.13.0 | 13.2 | cp313 |

## Features

- SageAttention 2.1.2
- Compiled for CUDA Compute Capability 7.5 (SM75)
- Tested on Google Colab Free (Tesla T4)

## Supported GPU Architecture

The wheels are compiled specifically for **CUDA Compute Capability 7.5 (SM75)**.

| Compute Capability | Architecture | Example GPUs |
| --- | --- | --- |
| **7.5** | Turing | Tesla T4, RTX 2060, RTX 2070, RTX 2080, GTX 16xx |

> **Note:** These wheels were built and tested on the free **NVIDIA Tesla T4 (SM75)** available in Google Colab.

## Installation

Pick a build from `legacy_wheels/` or `optimized_wheels/` depending on your workflow (see [Repository structure](#repository-structure)).

### legacy_wheels — PyTorch 2.11.0 + CUDA 13.0

```
# Uninstall conflicting CUDA 12 RAPIDS packages
!pip uninstall -q -y \
    libraft-cu12 \
    libcuvs-cu12 \
    libcuml-cu12 \
    cudf-cu12 \
    cuml-cu12

# Install CUDA 13 RAPIDS packages (optional)
!pip install -U \
    cudf-cu13 \
    cuml-cu13 \
    cuvs-cu13 \
    cuda-python \
    --extra-index-url https://pypi.nvidia.com

# Install PyTorch + CUDA 13
!pip install -U \
    torch==2.11.0 \
    torchvision==0.26.0 \
    torchaudio==2.11.0 \
    xformers==0.0.35 \
    --index-url https://download.pytorch.org/whl/cu130
```

```
%cd /content

!wget -O sageattention-2.1.2-cp313-cp313-linux_x86_64.whl \
https://github.com/netrunner-exe/SageAttention2-Colab-Wheels/raw/main/legacy_wheels/colab-torch-cp313-2.11.0%2Bcu130/sageattention-2.1.2-cp313-cp313-linux_x86_64.whl

!pip install sageattention-2.1.2-cp313-cp313-linux_x86_64.whl
```

### legacy_wheels — PyTorch 2.13.0 + CUDA 13.2

```
# Uninstall conflicting CUDA 12 RAPIDS packages
!pip uninstall -y \
    libraft-cu12 \
    libcuvs-cu12 \
    libcuml-cu12 \
    cudf-cu12 \
    cuml-cu12

!pip uninstall -y torchaudio

# Install CUDA 13 RAPIDS packages (optional)
!pip install -U \
    cudf-cu13 \
    cuml-cu13 \
    cuvs-cu13 \
    cuda-python \
    --extra-index-url https://pypi.nvidia.com

# Install PyTorch + CUDA 13.2
!pip install -U --force-reinstall \
    torch==2.13.0 \
    torchvision==0.28.0 \
    torchaudio==2.13.0 \
    --index-url https://download.pytorch.org/whl/cu132

!pip install -U --pre torchaudio \
    --index-url https://download.pytorch.org/whl/nightly/cu132

!pip install -U xformers==0.0.35 \
    --index-url https://download.pytorch.org/whl/cu130
```

```
%cd /content

!wget -O sageattention-2.1.2-cp313-cp313-linux_x86_64.whl \
https://github.com/netrunner-exe/SageAttention2-Colab-Wheels/raw/main/legacy_wheels/colab-torch-cp313-2.13.0%2Bcu132/sageattention-2.1.2-cp313-cp313-linux_x86_64.whl

!pip install sageattention-2.1.2-cp313-cp313-linux_x86_64.whl
```

### legacy_wheels — Default Google Colab (PyTorch 2.11.0 + CUDA 12.8)

```
%cd /content

!wget -O sageattention-2.1.2-cp313-cp313-linux_x86_64.whl \
https://github.com/netrunner-exe/SageAttention2-Colab-Wheels/raw/main/legacy_wheels/colab-torch-cp313-2.11.0%2Bcu128/sageattention-2.1.2-cp313-cp313-linux_x86_64.whl

!pip install sageattention-2.1.2-cp313-cp313-linux_x86_64.whl
```

### optimized_wheels

Same pip/RAPIDS/PyTorch preparation steps as above, matched to the corresponding CUDA version. Fetch the wheel from the `optimized_wheels` folder instead, e.g.:

```
%cd /content

!wget -O sageattention-2.1.2-cp313-cp313-linux_x86_64.whl \
https://github.com/netrunner-exe/SageAttention2-Colab-Wheels/raw/main/optimized_wheels/colab-torch-cp313-2.11.0%2Bcu130/sageattention-2.1.2-cp313-cp313-linux_x86_64.whl

!pip install sageattention-2.1.2-cp313-cp313-linux_x86_64.whl
```

## Usage

In ComfyUI, insert the **Patch Sage Attention KJ** node between the diffusion model loader and the sampler, then set **Mode** to **Auto**.

```
Model Loader → Patch Sage Attention KJ → Sampler
```

Using this node is recommended instead of launching ComfyUI with the `--use-sage-attention` flag.

When testing **legacy_wheels** SageAttention with **MiniMax H3**, launching ComfyUI with `--use-sage-attention` produced the following error:

```
[ERROR] Error running sage attention: Input tensors must be in dtype of torch.float16 or torch.bfloat16, using pytorch attention instead.
```

In this case, ComfyUI falls back to the default PyTorch attention implementation.

## Performance

The following benchmarks were performed using the **legacy_wheels** build with the standard **MiniMax H3** workflow and a fixed random seed.

> **Note:** Based on practical use, **CUDA 13.0** and **CUDA 13.2** delivers excellent performance.

### Workflow

- Model: `minimax_h3_fl2va_pruned_int8_convrot.safetensors`
- Aspect ratio: **16:9 (Widescreen)**
- Megapixels: **0.4**
- Duration: **5.0 s**
- Noise seed: **556589502035082**
- Scheduler: **res_multistep simple**
- Steps: **20**

### PyTorch 2.13.0 + CUDA 13.0

**Environment**

- PyTorch: **2.13.0**
- CUDA: **13.0**
- GPU: **Tesla T4**
- xFormers: **0.0.35**
- SageAttention: **2.1.2**

| Configuration | Execution Time |
| --- | --- |
| SageAttention 2.1.2 + Patch Sage Attention KJ | **00:21:45** |
| Default PyTorch attention | **00:49:43** |

### PyTorch 2.11.0 + CUDA 12.8

**Environment**

- PyTorch: **2.11.0**
- CUDA: **12.8**
- GPU: **Tesla T4**
- xFormers: **0.0.35**
- SageAttention: **2.1.2**

| Configuration | Execution Time |
| --- | --- |
| SageAttention 2.1.2 + Patch Sage Attention KJ | **00:35:03** |
| Default PyTorch attention | **00:58:32** |

> **Note:** Benchmarks were performed on the free Google Colab Tesla T4 runtime using the workflow described above. Actual performance may vary depending on the workflow and software versions.

## Source

- `legacy_wheels`: <https://github.com/Ph0rk0z/SageAttention2>
- `optimized_wheels`: <https://github.com/1506086927/SageAttention2_Optimized_Test>

## Disclaimer

These are unofficial community builds and are not affiliated with the original SageAttention project.
