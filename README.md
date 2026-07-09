# Puranik Yashaswin Sharma

A model behaving correctly is not the same claim as a model being aligned. One is 
observed, the other is inferred, and most of what passes for interpretability 
collapses that distinction. I work on not collapsing it: finding the actual 
computational structure behind a behavior, and verifying it rather than trusting it.

The same instinct shows up as systems work. I don't fully trust an abstraction I 
haven't implemented myself, so a fair amount of what's below is built from the 
metal up, not because it's efficient, but because it's the only way to know a 
number is real.

CS Undergrad @ Woxsen University | Core Contributor: **[TransformerLens](https://github.com/TransformerLensOrg/TransformerLens)** & **[SAELens](https://github.com/decoderesearch/SAELens)**

---

### Work

**[ioi-circuit-llama](https://github.com/puranikyashaswin/ioi-circuit-llama)**
Per-layer EAP-IG circuit discovery for indirect object identification on Llama-3.2-1B. Recovered a two-segment circuit (layers 0 to 8, layers 8 to 14) at 0.831 faithfulness against a 0.393 random baseline, with 0.556 Jaccard stability across seeds. The first version of the patching metric gave near-1.0 faithfulness even for random layer masks, which turned out to mean the metric was broken, not the circuit. Fixed by patching the block contribution (output minus input) rather than the full hidden state.

**[AutoCircuit](https://github.com/puranikyashaswin/AutoCircuit)**
Automated causal circuit discovery on GPT-2 Small. Scores all 156 components via activation patching. A 3-component circuit recovers 98.2% of correct IOI behavior, and a single component, mlp_L0, recovers 95.4% on its own. 99.6% search space reduction against exhaustive search.

**[bare-metal-transformer](https://github.com/puranikyashaswin/bare-metal-transformer)**
Transformer inference in pure C++. Zero ML dependencies, no PyTorch, no GGML. Flat KV cache via malloc, matmul with 16-wide ARM NEON FMA unrolling, i-k-j loop ordering. 125 tok/s vs PyTorch's single-threaded 113 tok/s on TinyStories-33M.

**[gqa-inference-engine](https://github.com/puranikyashaswin/gqa-inference-engine)**
From-scratch replication of Grouped Query Attention (arXiv:2305.13245) with KV caching, zero use of `nn.MultiheadAttention`. Natively resolves causal mask shape mismatches during cached decoding. 4x KV cache footprint reduction (1024 KiB to 256 KiB) and up to 4.7x generation speedup on CPU.

**[gpt2-hallucination-probe](https://github.com/puranikyashaswin/gpt2-hallucination-probe)**
Linear probing across all 12 layers of GPT-2 Small on a custom 46-prompt, 3-tier dataset. Peak AUROC 0.616 at Layer 0, dropping to chance on syntax-matched controls. After correcting a validation data leak, overall CV AUROC drops to 0.544, confirming the probe reads surface lexical artifacts, not epistemic state. Documented as a negative result because the negative result is the finding.

---

### Contributions

**[TransformerLens #1479](https://github.com/TransformerLensOrg/TransformerLens/pull/1479)**
TransformerBridge architecture adapter for BD3LM, a block-diffusion model with adaLN timestep conditioning and non-causal block-diffusion attention masking. Verified exact logit parity against the reference HF implementation.

**[TransformerLens #1162](https://github.com/TransformerLensOrg/TransformerLens/pull/1162)**
Fixed TinyStories weight loading. Positional embeddings were trimmed from a 2048 to 512 context length inside the conversion functions after HF configs reported the wrong context length.

**[SAELens #627](https://github.com/decoderesearch/SAELens/pull/627)**
Added an early runtime ValueError when cache activation context size exceeds training tokens, replacing a silent downstream failure with a clear error at the point of misconfiguration.

**[SAELens #628](https://github.com/decoderesearch/SAELens/pull/628)** · **[n8n #25105](https://github.com/n8n-io/n8n/pull/25105)**

---

### Stack

Python, C/C++, PyTorch, TransformerLens, SAELens
