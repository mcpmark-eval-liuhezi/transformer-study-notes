# Attention Is All You Need — Study Notes

- **Paper title:** Attention Is All You Need (Vaswani et al., 2017)
- **arXiv ID:** 1706.03762
- **Headline BLEU scores (from the paper's abstract):**
  - WMT 2014 English-to-German: **28.4 BLEU** (big model; >2 BLEU over the previous best, including ensembles)
  - WMT 2014 English-to-French: **41.8 BLEU** (single-model state of the art, trained 3.5 days on 8 GPUs)

## Topics covered (one per sub-issue of the study tracker, #2)

- **Model architecture (Section 3)** — encoder/decoder stacks of $N = 6$ layers, $d_{model} = 512$, multi-head attention with $h = 8$ heads ($d_k = d_v = 64$), scaled dot-product attention $\mathrm{softmax}(QK^T/\sqrt{d_k})V$.
- **Training setup (Section 5)** — WMT 2014 EN-DE (~4.5M sentence pairs, ~37k BPE vocabulary) and EN-FR (36M sentences, 32k word-piece vocabulary); 8× NVIDIA P100 GPUs; base model 100,000 steps / 12 hours, big model 300,000 steps / 3.5 days; Adam with warmup_steps = 4000, $P_{drop} = 0.1$, label smoothing $\epsilon_{ls} = 0.1$.
- **Results and evaluation (Section 6)** — newstest2014 BLEU: 28.4 (EN-DE big) and 41.8 (EN-FR big); base model 27.3 / 38.1; training cost $3.3 \cdot 10^{18}$ FLOPs (base) vs $2.3 \cdot 10^{19}$ (big); beam search with beam size 4 and length penalty $\alpha = 0.6$; checkpoint averaging of the last 5 (base) / 20 (big) checkpoints.
