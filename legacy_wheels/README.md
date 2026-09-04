# Legacy Wheels

Wheels compiled from **[Ph0rk0z/SageAttention2](https://github.com/Ph0rk0z/SageAttention2)**.

## Builds

| Folder | PyTorch | CUDA | Python |
| --- | --- | --- | --- |
| `colab-torch-cp312-2.11.0+cu128` | 2.11.0 | 12.8 | 3.12 |
| `colab-torch-cp313-2.11.0+cu128` | 2.11.0 | 12.8 | 3.13 |
| `colab-torch-cp312-2.11.0+cu130` | 2.11.0 | 13.0 | 3.12 |
| `colab-torch-cp313-2.11.0+cu130` | 2.11.0 | 13.0 | 3.13 |
| `colab-torch-cp313-2.13.0+cu132` | 2.13.0 | 13.2 | 3.13 |

Wheel filename in all folders: `sageattention-2.1.2-cp313-cp313-linux_x86_64.whl`

## Known issues

- **Krea 2** — confirmed broken.
- **MiniMax H3** — confirmed working.

If your workflow uses Krea 2 or a Flux-family DiT model, use `optimized_wheels` instead.
