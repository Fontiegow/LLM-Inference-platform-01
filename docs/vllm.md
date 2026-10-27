# vLLM Serving Notes (Milestone 1)

## Hardware
- GPU: NVIDIA GeForce RTX 3050 Ti Laptop (4 GB VRAM)
- Host: Windows 11 + WSL2 (Ubuntu 24.04) + Docker Desktop
- Docker disk image: `E:\DockerResources`
- Hugging Face cache: `E:\huggingface-cache` (junction at `%USERPROFILE%\.cache\huggingface`)

## Image & Model
- Image: `vllm/vllm-openai:latest` (v0.30.0 observed)
- Model: `Qwen/Qwen2.5-0.5B-Instruct`
- dtype: bfloat16
- No quantization

## Working launch command

```powershell
docker run --rm -it `
  --gpus all `
  --ipc=host `
  -p 8000:8000 `
  -v "${env:USERPROFILE}\.cache\huggingface:/root/.cache/huggingface" `
  vllm/vllm-openai:latest `
  --model Qwen/Qwen2.5-0.5B-Instruct `
  --host 0.0.0.0 `
  --port 8000 `
  --gpu-memory-utilization 0.75 `
  --max-model-len 2048 `
  --enforce-eager