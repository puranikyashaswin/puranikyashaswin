# Puranik Yashaswin Sharma

I work on ML systems from two ends of the stack: 
**Internals** (Reverse-engineering representations, mechanistic interpretability) and **Systems** (Bare-metal inference, memory bandwidth optimization).

CS Undergrad @ Woxsen University | Core Contributor: **[TransformerLens](#)** & **[SAELens](#)**

---

###  The Stack

* **Internals:** Activation patching, linear probing, causal circuit discovery, equation-to-code architecture replication.
* **Systems:** C/C++, ARM NEON SIMD intrinsics, flat memory allocation, cache-line streaming.
* **Tools:** PyTorch, wgpu/Metal, NetworkX.

---

###  Work

* **[AutoCircuit](https://github.com/puranikyashaswin/AutoCircuit)**
  Automated causal circuit discovery on GPT-2 Small. Scores all 156 components via activation patching. Found a minimal 3-component circuit recovering **93.4% of IOI performance**. 90 pairwise passes vs. ~24,000 exhaustivea **99.6% reduction** in search space.

* **[bare-metal-transformer](https://github.com/puranikyashaswin/bare-metal-transformer)**
  Transformer inference in pure C++. Zero ML dependencies (No PyTorch, no GGML). Flat KV cache via malloc, matmul with 16-wide ARM NEON FMA unrolling, and i-k-j loop ordering. **125 tok/s** vs PyTorch's single-threaded 113 tok/s on TinyStories-33M.

* **[gqa-inference-engine](https://github.com/puranikyashaswin/gqa-inference-engine)**
  Equation-to-code replication of Grouped Query Attention (arXiv:2305.13245). Zero use of `nn.MultiheadAttention`. Handled causal mask shape mismatches during cached decoding natively. Verified **4x KV cache reduction** (1048KB → 262KB) and **16x generation speedup**.

* **[gpt2-hallucination-probe](https://github.com/puranikyashaswin/gpt2-hallucination-probe)**
  Linear probing across all 12 residual stream layers of GPT-2 Small using a custom 46-prompt, 3-tier dataset. Peak AUROC 0.708 at Layer 0, dropping to chance on syntax-matched controls. **Finding:** The probe exploits surface lexical artifacts, not epistemic state. Documented as a legitimate negative result.

* **[rusty](https://github.com/puranikyashaswin/rusty)**
  *Ongoing:* GPU-accelerated ML training framework in pure Rust using wgpu/Metal.

---

> Self-directed, shipping code, and always looking for the next hard bottleneck.
