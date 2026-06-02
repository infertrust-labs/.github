<p align="center">
  <img src="https://raw.githubusercontent.com/infertrust-labs/.github/main/profile/assets/infertrust-logo.png" width="120" alt="InferTrust Labs logo">
</p>

<h1 align="center">InferTrust Labs</h1>

<p align="center">
  Open-source security tooling for trustworthy AI inference on Linux.
</p>

<p align="center">
  <strong>Runtime integrity. Supply-chain verification. Linux-native observability.</strong>
</p>

<p align="center">
  <a href="https://github.com/infertrust-labs/infertrust-runtime">
    <img src="https://img.shields.io/badge/project-infertrust--runtime-blue" alt="InferTrust Runtime">
  </a>
  <a href="https://github.com/infertrust-labs/infertrust">
    <img src="https://img.shields.io/badge/project-infertrust-teal" alt="InferTrust">
  </a>
  <img src="https://img.shields.io/badge/focus-Linux%20Security-brightgreen" alt="Linux Security">
  <img src="https://img.shields.io/badge/topics-eBPF%20%7C%20SBOM%20%7C%20AI%20Security-purple" alt="Topics">
  <img src="https://img.shields.io/badge/license-Apache%202.0-lightgrey" alt="License">
</p>

---

## What we are building

InferTrust Labs builds open-source tools for verifying and monitoring Linux-based AI inference stacks.

Modern AI inference systems depend on more than application code. A typical deployment may include:

```text
Linux kernel
↓
GPU kernel modules
↓
CUDA / NCCL
↓
PyTorch / Triton
↓
vLLM or SGLang
↓
Containers
↓
Model weights
↓
Tokenizers
↓
LoRA adapters
↓
Inference endpoint
```

Each layer affects the trustworthiness of the final service.

Our core question is simple:

> Can we prove what actually ran?

---

## Current projects

| Repository | Status | Focus |
|---|---:|---|
| [`infertrust-runtime`](https://github.com/infertrust-labs/infertrust-runtime) | Active | eBPF-based runtime integrity monitoring for Linux AI serving stacks |
| [`infertrust`](https://github.com/infertrust-labs/infertrust) | Active | AI inference supply-chain verification, AI-aware SBOMs, model provenance, and attestation reports |

---

## InferTrust Runtime

[`infertrust-runtime`](https://github.com/infertrust-labs/infertrust-runtime) is focused on runtime integrity.

It explores how Linux kernel observability can help detect unauthorized changes in AI serving stacks such as vLLM, SGLang, and PyTorch.

It watches for signals such as:

- model file access
- tokenizer access
- LoRA adapter access
- shared library loads
- process execution
- container-related execution
- suspicious file replacement
- selected kernel module activity

The goal is to connect Linux runtime events to AI-specific security questions:

```text
Did the inference process load the expected model?
Did it load an unexpected LoRA adapter?
Did it open a modified tokenizer?
Did it load an unexpected shared object?
Did the running process match the approved deployment profile?
```

---

## InferTrust

[`infertrust`](https://github.com/infertrust-labs/infertrust) is focused on AI inference supply-chain verification.

It is designed to help operators generate evidence about the full inference stack, including:

- Linux distribution and kernel version
- GPU kernel modules
- CUDA and NCCL versions
- PyTorch, Triton, vLLM, and SGLang metadata
- container image digests
- OCI signature checks
- model file hashes
- tokenizer hashes
- LoRA adapter hashes
- AI-aware SBOM output
- attestation reports

The goal is to extend familiar Linux supply-chain practices to AI-specific artifacts such as model weights, tokenizers, quantized checkpoints, and adapters.

---

## Why this matters

AI inference is becoming a major Linux workload.

Many teams can answer:

> Is the endpoint responding?

Fewer can answer:

> Which model, container, libraries, kernel modules, and runtime artifacts were actually used?

That gap matters.

A service can appear healthy while loading an unexpected model, modified tokenizer, unsigned adapter, changed container image, or unapproved shared library.

InferTrust Labs exists to make those risks visible.

---

## Threat scenarios we care about

| Scenario | Risk |
|---|---|
| Model file replacement | The service runs a different model than expected |
| LoRA adapter substitution | Model behavior changes through an unauthorized adapter |
| Tokenizer drift | Input and output behavior changes without a model change |
| Shared library injection | Runtime code changes below the application layer |
| Container drift | The running image does not match the approved digest |
| Kernel module changes | GPU runtime trust is weakened or unknown |
| Unsigned artifacts | Critical inference components lack provenance |

---

## Design principles

| Principle | Meaning |
|---|---|
| Open source first | Code, examples, policies, and reports should be public and inspectable |
| Linux-native | Use standard Linux mechanisms where possible |
| Evidence-driven | Every finding should map back to observable runtime or supply-chain evidence |
| Framework-aware | Model weights, tokenizers, and LoRA adapters should be treated as first-class security artifacts |
| Practical | The tools should be useful to Linux operators, platform teams, and AI infrastructure teams |
| Auditable | Core logic should be simple enough to review and reason about |

---

## Early roadmap

```text
1. Define AI inference supply-chain and runtime integrity threat models
2. Build baseline policy formats
3. Generate AI-aware SBOMs for inference deployments
4. Hash and verify model, tokenizer, and LoRA artifacts
5. Collect Linux runtime evidence from /proc, /sys, lsmod, and modinfo
6. Verify container provenance and OCI signatures
7. Capture runtime events with eBPF
8. Detect unexpected model, adapter, and shared library access
9. Generate clean vs drifted attestation reports
10. Publish reproducible vLLM, SGLang, and PyTorch demo traces
```

---

## Example runtime warning

```text
INTEGRITY WARNING

Process: vllm
Event: unexpected_model_artifact
File: /models/llama-3.1-8b/unknown_adapter.safetensors
Action: opened by inference process
Status: untrusted runtime drift detected
```

---

## Example attestation question

```text
Can we prove which model, tokenizer, container, GPU runtime, and Linux components were present when this inference service was scanned?
```

That is the problem InferTrust Labs is working on.

---

## Who this is for

InferTrust Labs is for:

- Linux security engineers
- AI infrastructure engineers
- platform engineers
- DevSecOps teams
- runtime security researchers
- supply-chain security practitioners
- open-source maintainers

This problem sits between Linux security, AI infrastructure, DevSecOps, and supply-chain assurance.

---

## Contributing

This work is early and intentionally open.

Useful contributions include:

- eBPF event collection
- BPF LSM experiments
- vLLM and SGLang runtime testing
- model artifact policy design
- AI-aware SBOM design
- attestation report formats
- container provenance examples
- documentation
- demo traces
- threat modeling

---

## License

Projects under InferTrust Labs are released under open-source licenses, starting with Apache License 2.0 unless otherwise noted.

---

## Mission

InferTrust Labs exists to make AI inference on Linux more observable, verifiable, and trustworthy.

The mission is simple:

> Prove what actually ran.
