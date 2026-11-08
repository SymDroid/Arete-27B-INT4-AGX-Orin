---
license: apache-2.0
base_model: NousResearch/Arete-27B
pipeline_tag: text-generation
language:
- en
tags:
- quantization
- int4
- compressed-tensors
- marlin
- jetson
- jetson-agx-orin
- vllm
- mtp
---
# Arete 27B INT4 for NVIDIA Jetson AGX Orin

**Publisher / quantization:** [SymDroid](https://github.com/symdroid)  
**Original model:** [NousResearch/Arete-27B](https://huggingface.co/NousResearch/Arete-27B)  
**Underlying model:** [Qwen/Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)  
**Weights:** [Hugging Face](https://huggingface.co/symdroid/Arete-27B-INT4-AGX-Orin)  
**Code / documentation:** [GitHub](https://github.com/symdroid/Arete-27B-INT4-AGX-Orin)

This is a **third-party W4A16 INT4 quantization** of Nous Research's Arete-27B,
packaged for **text-only vLLM inference on NVIDIA Jetson AGX Orin**. It is **not**
an official Nous Research, Alibaba, or NVIDIA release.

## Checkpoint details

- Approximate weight files: 19.47 GB in total (local checkpoint including supporting files).
- Architecture identifier: `qwen3_5` (as in `config.json`); model lineage is Qwen3.8-27B.
- Quantization: 4-bit weights, 16-bit activations; `compressed-tensors` / `pack-quantized`, group size 128.
- The checkpoint index includes **15 MTP-named tensors**, including `mtp.fc.weight`.
- BF16 MTP head included; MTP execution is backend/version dependent.
- Six indexed safetensors shards; tokenizer and configuration included.
- Tested target: Jetson AGX Orin with vLLM for language-model inference.
- Internal SymDroid served-model identifier: `symarete38` (not the public release name).

## Running on Jetson AGX Orin

The deployed SymDroid instance used port 8011, `--language-model-only`,
`--gpu-memory-utilization 0.60`, `--max-model-len 2048`, and
`--no-enable-prefix-caching` during initial validation. These are **deployment-specific**
settings, not claims of maximum supported context or a universal turnkey launch
command. Choose your own vLLM build, container, quantization compatibility,
GPU memory budget, and MTP/speculative decoding configuration. The presence of
MTP tensors does not by itself enable speculative decoding.

**Scope:** text-only inference validated; multimodal execution, throughput,
long-context stability and portable MTP performance are **not benchmarked here**.
Do not interpret any upstream benchmark as a benchmark of this quantization.

## Provenance and license

- Nous Research developed Arete-27B by post-training Qwen3.8-27B.
- SymDroid performed an independent INT4 quantization and assembled the MTP-containing checkpoint.
- The original works are licensed under **Apache License 2.0**.
- Original upstream license texts are reproduced in `licenses/`, and attribution
  plus the nature of the modification are recorded in `NOTICE`.
- Model weights are supplied AS IS; validate locally for your own use.
