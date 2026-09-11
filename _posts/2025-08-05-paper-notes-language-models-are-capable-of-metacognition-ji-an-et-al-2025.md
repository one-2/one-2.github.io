---
title: "Paper notes: Language Models Are Capable of Metacognition (Ji-An et al., 2025)"
date: 2025-08-05
permalink: /posts/2025/08/paper-notes-language-models-are-capable-of-metacognition-ji-an-et-al-2025/
categories:
  - Paper Notes
  - General reading group
tags:
  - artificial intelligence
  - computer science
  - LLM
  - metacognition
  - methodology
  - research
  - technology
---

Welcome to Paper Notes, the vessel for the thoughts and reflections of our weekly reading group.

This week we read *Language Models Are Capable of Metacognition*.[^1] The research group is comprised of computational and cognitive neuroscientists from Georgia Tech, UC San Diego, and New York University. The lead authors are both PhD students with interests in computational neuroscience.

## Views on the paper

Each week, I ask participants for a brief reflection on the contents of the selected paper.

Our group had a spirited discussion about the paper. Here are some views expressed by our members:

- Natsu: Both the explicit and implicit metacognition demonstrated here are explainable as in-context learning (see the GPT-3 paper).
- Jack: "The finding that these models can alter their activations while producing identical outputs (when motivated by a goal) exposes gaps in existing monitoring methods. It also raises the exciting prospect of enhanced model performance via reflection and metacognition."
- Stephen: "The paper demonstrates models could have some degree of metacognitive agency - modulating their processing patterns in pursuit of a goal. Implicit metacognition is some evidence that a model with its own goals could trick our interpretability tools to achieve them, lending weight to next-generation problems[^2][^3] in AI control and interpretability risks."
- Dylan: "I liked having other people to talk to about the more esoteric parts of machine learning! It felt nice having people to demystify the process with."

## Post-discussion summary and analysis

We also provide a synthesis of the paper discussion and some commentary.

The paper shows that models' activation patterns shift to maximise a reward function defined by few-shot prompting of the model's own generation traces and an associated activation-derived score. This activation conditioning occurs in the "explicit case", when the model changes the tokens it outputs. Surprisingly, this behaviour also occurs in the "implicit case", where researchers copied an output into the prompt and ran separate forward passes on the pair under different label goals. Across many such trials, the model's score reduces when told to reduce, and increases when told to increase.

This is cognitive conditioning, wherein the model's activation patterns adapt according to context. This is a necessary, but insufficient, condition for metacognition, traditionally defined as self-awareness of, and self-control over, thinking.[^4] Metacognition would require additionally a model-internal cognitive routing mechanism which anticipated the effect of different routes and selected between them to achieve a goal. That is, to satisfy metacognition, cognitive conditioning must be internal to the model, rather than provided externally.

To illuminate the practical difference between cognitive conditioning and metacognition, consider that there are many plausible avenues for a model to minimise its interpretability score which do not use metacognition. This point was astutely raised by Natsu during our meeting. Though the model may asymptotically reduce its score by conditioning its sampling on the implicit reward surface, generating a reward-maximising response each turn, it has not used any internal monitoring and modulation mechanisms. Therefore, metacognition has not occurred.

The experimental design does not allow for the identification of metacognitive capabilities in the model. The model may have optimised its responses according to spurious correlations not related to true cognitive patterns and conditioned generation on them, improving score without any metacognitive function. Furthermore, the highly structured implicit case is not reflective of natural LLM inference environments. Hence, the experiments show that implicit cognitive conditioning is possible, but not that it currently occurs in real settings.

Hence, the paper demonstrates cognitive conditioning, a pre-metacognitive capability, and is best viewed as an indication of latent capability which could be further trained to develop full metacognition.

---

This blog was originally posted at <https://deep-network.org/2025/08/05/paper-notes-language-models-are-capable-of-metacognition-ji-an-et-al-2025/>

Citations:

[^1]: Li, J.-A., Xiong, H.-D., Wilson, R. C., Mattar, M. G., & Benna, M. K. (2025). Language models are capable of metacognitive monitoring and control of their internal activations. *arXiv*. <https://doi.org/10.48550/arXiv.2505.13763>
[^2]: AI Security Institute. (2025). Research areas in AI control (The Alignment Project by UK AISI). *AI Alignment Forum*. <https://www.alignmentforum.org/posts/rGcg4XDPDzBFuqNJz/the-alignment-project-by-uk-aisi-research-areas-in-ai-1>
[^3]: AI Security Institute. (2025). Research areas in interpretability (The Alignment Project by UK AISI). *AI Alignment Forum*. <https://www.alignmentforum.org/posts/dgcsY8CHcPQiZ5v8P/the-alignment-project-by-uk-aisi-interpretability>
[^4]: Bommasani, R., Hudson, D. A., Adeli, E., Altman, R., Arora, S., von Arx, S., ... & Liang, P. (2021). On the opportunities and risks of foundation models. *Proceedings of the 2021 ACM Conference on Fairness, Accountability, and Transparency*, 610–623. <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8187395/>
