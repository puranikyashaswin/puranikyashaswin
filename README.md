# Yashaswin Puranik Sharma

A model behaving correctly is not the same claim as a model being aligned. One is 
observed, the other is inferred, and most of what passes for interpretability 
collapses that distinction. I work on not collapsing it: finding the actual 
computational structure behind a behavior, and verifying it rather than trusting it.

The same instinct shows up as systems work. I don't fully trust an abstraction I 
haven't implemented myself, so a fair amount of what's below is built from the 
metal up, not because it's efficient, but because it's the only way to know a 
number is real.

CS undergrad @ Woxsen University · 5 merged PRs: [TransformerLens](https://github.com/TransformerLensOrg/TransformerLens), [SAELens](https://github.com/decoderesearch/SAELens), [n8n](https://github.com/n8n-io/n8n)

### Research and evaluation

| Project | Question | Result |
|---|---|---|
| [transfer_mech](https://github.com/puranikyashaswin/transfer_mech) | Does one injected activation vector carry program-repair information between code models? | No. On 215 held-out Java bugs the trained adapter did worse than no intervention: 51.6% vs 63.7%, p = 0.0013 |
| [AutoCircuit](https://github.com/puranikyashaswin/AutoCircuit) | Which GPT-2 Small components carry the IOI task? | A fixed 3-component circuit recovers 93.4% of the logit difference on 8 prompts (random 3: 2.7%) and 100.5% on 360 generated prompts (random 3: 7.5%) |
| [gpt2-hallucination-probe](https://github.com/puranikyashaswin/gpt2-hallucination-probe) | Can a linear probe on GPT-2's residual stream detect hallucination-prone prompts? | Inconclusive. Pair-held-out AUROC 0.67, 95% CI 0.49 to 0.87; the 0.616 peak is not significant after layer selection |
| [ioi-circuit-llama](https://github.com/puranikyashaswin/ioi-circuit-llama) | Does a layer-level IOI circuit exist in Llama-3.2-1B? | Layers [0, 9] reach 1.063 faithfulness but do not beat their own random masks (p = 0.09 to 0.18) |

Every transfer_mech number is recomputed from the raw logs by `make verify`, and CI runs it on every push.

### Systems

| Project | Result |
|---|---|
| [gqa-inference-engine](https://github.com/puranikyashaswin/gqa-inference-engine) | Grouped-query attention from scratch, matches torch SDPA to 3e-7; 4x smaller KV cache and 3.3x to 5.6x faster cached decoding for one attention layer on CPU |
| [bare-metal-transformer](https://github.com/puranikyashaswin/bare-metal-transformer) | Transformer inference in pure C++ with ARM NEON kernels; 138 tok/s single-threaded on TinyStories-33M, 96% of PyTorch's 144 tok/s |
| [Reex-1](https://github.com/puranikyashaswin/Reex-1) | 116M-parameter decoder pretrained on about 1.31B tokens and chat-tuned from scratch |

### Merged upstream

- [TransformerLens #1479](https://github.com/TransformerLensOrg/TransformerLens/pull/1479): TransformerBridge adapter for BD3LM, with logit parity against the Hugging Face model confirmed block by block
- [TransformerLens #1162](https://github.com/TransformerLensOrg/TransformerLens/pull/1162): TinyStories models trimmed to their real 512-token context
- [SAELens #627](https://github.com/decoderesearch/SAELens/pull/627): clear error when context size exceeds training tokens · [#628](https://github.com/decoderesearch/SAELens/pull/628): nested progress bars in Jupyter
- [n8n #25105](https://github.com/n8n-io/n8n/pull/25105): Miro OAuth2 scope field made visible

### Stack

![Python](https://img.shields.io/badge/Python-30363d?style=flat-square) ![PyTorch](https://img.shields.io/badge/PyTorch-30363d?style=flat-square) ![C++](https://img.shields.io/badge/C++-30363d?style=flat-square) ![Java](https://img.shields.io/badge/Java-30363d?style=flat-square) ![TransformerLens](https://img.shields.io/badge/TransformerLens-30363d?style=flat-square) ![SAELens](https://img.shields.io/badge/SAELens-30363d?style=flat-square) ![FastAPI](https://img.shields.io/badge/FastAPI-30363d?style=flat-square) ![LangGraph](https://img.shields.io/badge/LangGraph-30363d?style=flat-square) ![JUnit](https://img.shields.io/badge/JUnit-30363d?style=flat-square) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-30363d?style=flat-square)
