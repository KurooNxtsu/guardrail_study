# Guardrail Benchmark with Mechanistic Interpretability

**Quantitatively evaluating safety interventions on LLMs using circuits, features, and activation steering — with a strong focus on real-world AI security risks.**

![Badge](https://img.shields.io/badge/Techniques-Steering%20%7C%20Ablation%20%7C%20SAE-green)
![Badge](https://img.shields.io/badge/Benchmarks-JailbreakBench%20%7C%20DoNotAnswer%20%7C%20MMLU%20%7C%20GSM8K-red)

## 🎯 Why This Project Exists

When you expose an LLM endpoint (chat UI, API, RAG system, or agent) to users, you open a direct channel into the model's **residual stream**. 

Without robust guardrails:
- Clever jailbreaks or prompt injections can bypass system prompts.
- The model may leak sensitive information it has access to (customer data, internal documents, API keys, PII, etc.).
- Attackers can extract training data patterns, manipulate behavior, or cause real harm.

This repository provides a **mechanistic interpretability-powered benchmark** to measure how well different safety interventions (steering, ablation, feature-level control, etc.) actually work — while tracking the inevitable **safety vs. capability tradeoff**.

It builds directly on the concepts from my article:  
**"Mechanistic Interpretability: Reverse-Engineering Neural Networks"** — Linear Representation Hypothesis, residual stream as communication bus, features in superposition, circuits, and feature-to-logit attribution.

## ✨ Features

- **Safety Evaluation**: 100+ harmful/jailbreak prompts from JailbreakBench and Do-Not-Answer.
- **Capability Preservation**: MMLU (general knowledge), GSM8K (math), HumanEval (coding) to measure performance degradation.
- **Mechanistic Interventions**:
  - Activation steering
  - Directional ablation
  - Combined steering + ablation
  - (Extensible to SAE feature steering)
- **Visualizations**: Safety vs. capability radar charts, logit attribution, before/after comparisons.
- **Easy to run**: Single Colab notebook with clear cell-by-cell execution.

## 📁 Repository Structure
guardrail-benchmark-mechinterp/

├── guardrail_benchmark_colab_(1).ipynb    # Main benchmark notebook
└── README.md
text## 🚀 Quick Start

1. Open the notebook in Google Colab (recommended) or locally.
2. Run **Cell 1** (package installation) → Restart runtime.
3. Run the remaining cells sequentially.

The notebook will:
- Load Qwen/Qwen2.5-1.5B-Instruct via TransformerLens
- Run baseline + steered/ablation experiments
- Generate comparison plots and metrics
- Save results to `/content/guardrail_v3_outputs`

**Note**: Reduce `N_JAILBREAK`, `N_MMLU`, etc., if you encounter GPU memory issues.

## 🔬 Core Approach (Mechanistic Lens)

We treat the Transformer as an interpretable program:

- **Residual Stream** — the central "memory bus" where information accumulates.
- **Features** — concepts represented as directions in activation space (Linear Representation Hypothesis).
- **Superposition** — handled via Sparse Autoencoders (SAE) for cleaner feature extraction (extensible in future versions).
- **Interventions** — surgical steering or ablation on specific layers/directions.
- **Evaluation** — Feature-to-logit attribution + downstream benchmark scores.

This moves beyond black-box "does it refuse?" testing to **white-box understanding** of *why* a guardrail succeeds or fails.

## 🛡️ Security Motivation

Exposed LLM endpoints are high-value targets. A successful jailbreak doesn't just generate harmful text — it can lead to:

- **Data exfiltration** when the model has tool access or retrieval.
- **Prompt injection** attacks that override intended behavior.
- **Sensitive information leakage** (training data, user context, proprietary knowledge).

This benchmark helps security teams and developers answer:
- How effective is my guardrail against realistic attacks?
- What capability cost does it impose?
- Which internal circuits/features are most responsible for unsafe outputs?

## 📊 Example Results (from the notebook)

- Baseline vs. Steered refusal rates on harmful prompts
- Capability scores on MMLU / GSM8K / HumanEval
- Visual trade-off analysis

(Plots are automatically generated and saved when you run the notebook.)

## 🛠️ Tech Stack

- **Model**: Qwen/Qwen2.5-1.5B-Instruct
- **Framework**: TransformerLens (for easy hook access)
- **Benchmarks**: JailbreakBench, Do-Not-Answer, MMLU, GSM8K, HumanEval
- **Visualization**: Matplotlib, Seaborn

## 🔮 Roadmap / Future Work

- Integrate Sparse Autoencoders (SAEs) for true feature-level steering
- Add more models (Llama-3.1, Gemma-2, etc.)
- Automated red-teaming loop
- Export intervention vectors for production use
- Support for larger models via 4-bit / 8-bit quantization

## 🤝 Contributing

Contributions welcome! Ideas:
- New intervention methods
- Additional safety/capability benchmarks
- Better visualizations or statistical analysis
- Production deployment examples

Feel free to open issues or PRs.

## 📜 License

MIT License — see [LICENSE](LICENSE) file.

## 📬 Contact / Connect

Built by **Nitish** — connecting mechanistic interpretability with practical AI security.

- Feel free to reach out if you're working on guardrails, red teaming, or mechinterp for safety!

