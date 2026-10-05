---
layout: default
title: Physics Agent
permalink: /projects/physics-agent/
---

[All projects]({{ '/projects/' | relative_url }})

# Physics Agent

I built a physics problem-solving agent that combines browser automation with local LLM inference. It reads problem text and diagrams, generates structured answers, and saves checkpoints so progress can be inspected across a run.

The notebook is designed to run Qwen3.5-27B directly on ICRN GPU compute using Hugging Face Transformers, with a 9B option for smaller GPU allocations. Running the model locally gives me control over model size, GPU memory usage, and the inference pipeline without depending on a hosted LLM API.

**Tools:** Python, PyTorch, Hugging Face Transformers, Qwen, Playwright.
