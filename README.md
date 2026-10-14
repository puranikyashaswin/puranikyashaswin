# Puranik Yashaswin Sharma

A model behaving correctly is not the same claim as a model being aligned. One is 
observed, the other is inferred, and most of what passes for interpretability 
collapses that distinction. I work on not collapsing it: finding the actual 
computational structure behind a behavior, and verifying it rather than trusting it.

The same instinct shows up as systems work. I don't fully trust an abstraction I 
haven't implemented myself, so a fair amount of what's below is built from the 
metal up, not because it's efficient, but because it's the only way to know a 
number is real.

CS Undergrad @ Woxsen University | Merged PRs: **[TransformerLens](https://github.com/TransformerLensOrg/TransformerLens)** & **[SAELens](https://github.com/decoderesearch/SAELens)**

---

### Work

**[transfer_mech](https://github.com/puranikyashaswin/transfer_mech)**
Pre-registered study of activation transfer for program repair (Qwen2.5-Coder 1.5B to 3B), scored by Java test suites on 215 held-out bugs. The trained adapter did worse than no intervention (51.6% vs 63.7%, p=0.0013) and failed to compile 10x more often. A 13-1 dev-split win did not replicate on test. `make verify` recomputes all 28 reported numbers from the raw logs, and CI runs it on every push.

**[ioi-circuit-llama](https://github.com/puranikyashaswin/ioi-circuit-llama)**
Layer-level circuit discovery for indirect object identification on Llama-3.2-1B: integrated gradients score each block's residual contribution, then contribution-delta patching tests the top layers. Re-run with current code, the circuit is layers [0, 9] on all three seeds at 1.063 faithfulness against a 0.393 random baseline, but it does not beat its own random masks (p = 0.09 to 0.18), and most of layer 0's effect is re-injecting the swapped name token. The first version of the patching metric gave near-1.0 faithfulness even for random layer masks, which turned out to mean the metric was broken, not the circuit. Fixed by patching the block contribution (output minus input) rather than the full hidden state.

**[AutoCircuit](https://github.com/puranikyashaswin/AutoCircuit)**
Automated causal circuit discovery on GPT-2 Small. Scores all 156 components via activation patching. A fixed 3-component circuit recovers 93.4% of the IOI logit difference on 8 prompts and 100.5% on 360 generated prompts (random 3 components: 7.5%). Edge search needs 42 instead of 11,298 patches per prompt (99.6% fewer). Found and fixed an abs() scoring bug that picked the wrong top component on 3 of 8 prompts.

**[bare-metal-transformer](https://github.com/puranikyashaswin/bare-metal-transformer)**
Transformer inference in pure C++. Zero ML dependencies, no PyTorch, no GGML. Flat KV cache via malloc, matmul with 16-wide ARM NEON FMA unrolling, i-k-j loop ordering. 138 tok/s single-threaded on TinyStories-33M, 96% of PyTorch's 144 tok/s.

**[gqa-inference-engine](https://github.com/puranikyashaswin/gqa-inference-engine)**
From-scratch replication of Grouped Query Attention (arXiv:2305.13245) with KV caching, zero use of `nn.MultiheadAttention`. Natively resolves causal mask shape mismatches during cached decoding. 4x KV cache footprint reduction (1024 KiB to 256 KiB) and 3.3x to 5.6x faster cached decoding for one attention layer on CPU.

**[gpt2-hallucination-probe](https://github.com/puranikyashaswin/gpt2-hallucination-probe)**
Linear probing across all 12 layers of GPT-2 Small on a custom 46-prompt, 3-tier dataset. Peak AUROC 0.616 at Layer 0 is not significant once the best-of-12 layer selection is accounted for (permutation p = 0.49). On matched pairs, naive leave-one-out gave 0.38; pair-held-out CV fixed that artifact and gave 0.67, still weak (95% CI 0.49-0.87). The dataset can't show that the probe detects hallucination, and it can't rule it out. Documented as a negative result because the negative result is the finding.

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
