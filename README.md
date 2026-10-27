# LLM Inference Platform

Focused, production-oriented LLM inference stack built incrementally on consumer hardware.

## Current status — Milestone 1 complete

- Single vLLM OpenAI-compatible server
- Model: `Qwen/Qwen2.5-0.5B-Instruct`
- Hardware: RTX 3050 Ti 4 GB (WSL2 + Docker Desktop)
- Verified: model load, `/v1/models`, `/v1/chat/completions`, GPU memory behaviour

See [docs/vllm.md](docs/vllm.md) for exact commands, memory numbers, and engineering notes.

## Quick start (Milestone 1)

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