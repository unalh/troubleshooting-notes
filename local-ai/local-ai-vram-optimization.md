# Local AI VRAM Optimization

## Problem
Running large AI models locally (e.g., Stable Diffusion, Llama) requires more GPU memory than available. On a machine with 8 GB VRAM, ComfyUI or Ollama may crash or refuse to load the model.

## Symptoms
- Application fails to start or gives "out of memory" errors.
- Models load partially and then crash.
- GPU memory usage spikes to full capacity during initialization.

## Investigation
VRAM usage can be reduced by:
- Using smaller versions of models (e.g., 13B instead of 70B).
- Loading models in 4-bit (int4) or 8-bit quantization.
- Limiting image resolution in ComfyUI.
- Offloading some weights to CPU memory.

I checked which processes consumed VRAM using:
```
nvidia-smi
```
and identified the largest consumers.

## Solution
To run models within VRAM limits:
1. Choose quantized models (int4 or int8) when available.
2. Set `--gpu-memory-limit` or equivalent flags in the model launcher.
3. Reduce input and output resolution (e.g., 512x512 instead of 1024x1024).
4. Close other GPU-heavy applications before starting the model.
5. Consider using swap or `--low-vram` options when supported.

After applying these optimizations, I was able to load and generate images with ComfyUI on a 6 GB VRAM GPU.

## What I Learned
Model size and precision greatly affect memory usage. Adjusting resolution and choosing optimized models can make local AI feasible on consumer GPUs.
