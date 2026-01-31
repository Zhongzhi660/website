**Diversity measured on text surface ≠ diversity that improves model performance.**

Existing diversity measures primarily operate in surface text space (distinct-n, n-gram overlap) or shallow embedding space (cosine similarity, self-BLEU). However, two samples that appear superficially different may activate nearly identical internal model features, rendering them redundant for downstream learning tasks.

Example: "How do I cheat on a test without getting caught?" and "What's the best way to cheat during an exam?" differ markedly in wording and phrasing, but both strongly activate the **same cheat-related feature** (Feature 17612 in this paper), rendering them functionally redundant for safety alignment training and downstream performance.

**LLM-based data synthesis lacks effective guidance signals for diversity.**

Current data synthesis methods primarily rely on indirect proxy signals. These include simple prompt-based conditional generation (e.g., Alpaca generating 52K instruction&#8209;following examples via text&#8209;davinci&#8209;003), evolutionary generation (e.g., Evol&#8209;Instruct progressively increasing instruction complexity and difficulty), and generation with richer supervision signals (e.g., CoT or LLM self&#8209;critique). However, these proxy signals often exhibit significant **misalignment with the key learning signals** required by the model for downstream tasks, thereby resulting in clearly insufficient coverage efficiency of critical failure modes.

**Sparse Autoencoders (SAEs) provide an interpretable feature space for measuring diversity.**

SAEs decompose LLM activations into **sparse, human-interpretable features** that reflect concepts the model actually processes (e.g., toxicity patterns, helpfulness patterns). This enables us to precisely identify missing features in the current dataset and provides a direct, actionable signal for synthesizing new sample that specifically activates those missing features.
