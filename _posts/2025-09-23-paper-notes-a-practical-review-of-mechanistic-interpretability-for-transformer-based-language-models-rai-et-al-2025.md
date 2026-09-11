---
title: "Paper notes: A Practical Review of Mechanistic Interpretability for Transformer-Based Language Models (Rai et al., 2025)"
date: 2025-09-23
permalink: /posts/2025/09/paper-notes-a-practical-review-of-mechanistic-interpretability-for-transformer-based-language-models-rai-et-al-2025/
excerpt: "On Friday the 5th of September, the general reading group continued its mechanistic interpretability sprint with *A Practical Review of Mechanistic Interpretability for Transformer-Based Language Models*. The research team comes from across several US universities, with one member from Salesforce Research. Its lead author is a PhD student, and its second author a PhD working in industry. The survey was posted on arXiv and presented as a tutorial at ICML 2025."
categories:
  - Paper Notes
  - General reading group
tags:
  - artificial intelligence
  - computer science
  - data science
  - hypothesis
  - LLM
  - mechanistic interpretability
  - research
  - technology
  - transformer
archive_hidden: true
---

On Friday the 5th of September, the general reading group continued its mechanistic interpretability sprint with *A Practical Review of Mechanistic Interpretability for Transformer-Based Language Models*.[^1] The research team comes from across several US universities, with one member from Salesforce Research. Its lead author is a PhD student, and its second author a PhD working in industry. The survey was posted on arXiv and presented as a tutorial at ICML 2025.[^2]

The preprint surveys mechanistic interpretability, with a focus on the workflow of MI research and open problems in the field.

## Hypotheses on the paper

This week we tried something a little different. Rather than discussing the paper, we set ourselves the challenge of generating hypotheses about its contents. Here are some of these hypotheses:

1. Observation: most MI techniques exclude feedforward, layernorm, and embedding matrices from their analysis.
   - Hypothesis: a hybrid method analysing feedforward, layernorm, and embedding matrices would provide a more faithful representation of causal mechanisms in the model.
   - Counter: this might require relaxing simplifying assumptions about representations (eg linear representation hypothesis).
2. Observation: superposition is prevalent in LLMs.
   - Hypothesis: superposition hurts robustness of behaviours targeted during post-training.
3. Observation: circular representations are more information-efficient for encoding cyclical relationships, like time.
   - Hypothesis: models learn trigonometric operations to process cyclical information.
4. Observation: the SHIFT technique removes non-human-interpretable features to improve generalisation.
   - Hypothesis: human-AI collaboration on a task would be easier when using SHIFT.
   - Hypothesis: models confidence measures would be more accurate when using SHIFT.
5. Observation: the model encodes the truth of context tokens in a feature.
   - Hypothesis: we can detect lying despite hidden misalignment using truth features.
   - Hypothesis: LLMs have an internal "truth uncertainty" feature more accurate, reliable, or robust to misalignment than logits.
   - Hypothesis: we could model misaligned behaviour from MI features to detect misaligned behaviour at runtime.

---

This blog was originally posted at <https://deep-network.org/2025/09/23/paper-notes-a-practical-review-of-mechanistic-interpretability-for-transformer-based-language-models-rai-et-al-2025/>

[^1]: Rai, D., Zhou, Y., Feng, S., Saparov, A., & Yao, Z. (2024). A practical review of mechanistic interpretability for transformer-based language models. arXiv preprint arXiv:2407.02646. <https://arxiv.org/abs/2407.02646>
[^2]: Rai, D., Zhou, Y., Feng, S., Saparov, A., & Yao, Z. (2025, July 13). ICML 2025 Tutorial on Mechanistic Interpretability for Language Models. <https://ziyu-yao-nlp-lab.github.io/ICML25-MI-Tutorial.github.io/>
