---
title: "Paper notes: Computation Through Neural Population Dynamics (Vyas et al., 2020)"
date: 2025-09-29
permalink: /posts/2025/09/paper-notes-computation-through-neural-population-dynamics-vyas-et-al-2020/
categories:
  - Paper Notes
  - Mathematics reading group
tags:
  - activations
  - artificial intelligence
  - computer science
  - dynamical systems
  - dynamical systems theory
  - interpretability
  - LLM
  - neural population dynamics
  - neurology
  - neuroscience
  - research
archive_hidden: true
---

Welcome to Paper Notes, where we record our groups' weekly discussions of innovative papers from across artificial intelligence.

On Monday the 15th of September and 22nd of September, our mathematics reading group continued its exploration of dynamical systems theory (DST) in neuroscience, reading *Computation Through Neural Population Dynamics*.[^1]

The authors are from Stanford University and work across bioengineering, electrical engineering, AI, and neurobiology. The first author is Saurabh Vyas, then a PhD student in bioengineering. The second author is Matthew D. Dolub, then a postdoctoral fellow. The other authors are David Sussillo, then an adjunct professor in electrical engineering at Stanford and a senior research scientist at Google, and the late Krishna Shenoy, then a prominent neuroscientist and the supervisor to Vyas and Dolub.

The paper was published in the 2020 edition of *[Annual Review of Neuroscience](https://www.annualreviews.org/content/journals/neuro)*.

## Views on the paper

### Neuroscience can inspire dynamical systems analysis of other black-box systems, like LLMs

Static analysis is revealing and sufficient when an algorithm's properties are well-understood and consistent. In the case of learned algorithms, such as those in the brain or LLM activation space, the properties are nebulous. In the absence of an understanding of the system's natural limits, static analysis is incomplete, and may be misleading. The paper emphasises the limitations of static approaches to neuroscience analysis, and this limitation also applies in AI interpretability - most obviously to top-down approaches like representation engineering.

In constrast, mechanistic interpretability (MI) could be viewed as a projective approximation to the system's true dynamics, and therefore a step towards a dynamical systems approach to interpretability. We first learn a projection of activation dynamics onto human semantics, and then try to identify algorithms in this projection. The algorithms we identify are an approximation to the dynamics of the model's processing. However, these techniques work in terms of human meaning, and we may misinterpret unintuitive dynamics, attributing behaviour to a sensible but spurious algorithm which is present in the SAE readouts but not important to model behaviour outside the tested support.

A pure dynamical systems approach to interpretability would avoid the projection to human semantics, describing the behaviour of learned algorithms in the original space and thereby preserving more information than MI's projective approach. Indeed, our member Peter is researching is in this area.

### Differences in pace between neuroscience and AI

We were surprised to learn that methods for linearising RNNs have only been introduced to neuroscience in the last decade, while RNNs have been present in machine learning since the 1980s. However, dynamical systems were only introduced to neuroscience in the 1990s, and DST neuroscience is still emerging from static approaches to fMRI analysis. Our surprise came from projecting AI's pace onto neuroscience. We noted that AI's pace is not a good estimator of other fields' pace, due to AI's scalability and rapid progress in recent years.

### Limitations to neuroscience interventions which are not present in AI interpretability research

Neuroscience interventions are more limited than mechanistic interpretability in intervention power; while we can ablate or stimulate an LLM's activations, our interventions on the brain are limited by ethics. This limits the engineering outcomes we can achieve in biological brains.

A second limitation on neuroengineering is retrieving generalisable measures of the brain's processing function. Running controlled experiments on LLMs is a matter of systematically modifying the textual input. This process in much more challenging in a brain context, where input is much richer. This may limit the generaliseability of laboratory-derived measures of brain behaviour.

### Extending dynamical modelling in neuroscience

We note that financial modelling uses Brownian stochastic differential equations (SDEs) to model securities behaviour. Adding stochastic movement to differential equations fitted to fMRI might improve the power of DST in neuroscience too. With SDEs, we might be able to fit dynamics more accurately or more robustly.

We could also extend the modelling by using non-linear dynamical systems, though with the usual pitfalls. Perhaps it could be accelerated using simplifying techniques like kernel tricks.

### The power of DST modelling across fields

We note that DST is a generally powerful modelling technique due to the time-variant structure of real-world phenomena. Indeed, algorithms are also fundamentally dynamical. One member observed that if a thing is not changing over time, "it is dead." In this sense, we can only extract certain types of information from static representations.

### DSTs are relatively less common in AI interpretability research

We conclude by noting that DST is less prevalent in LLM research, maybe due to the lack of dynamical systems in computer science and data science, where AI is rooted and often taught. Researchers in fields like neuroscience, physics, and econometrics are more engaged with dynamical systems as part of their work. As LLM research matures, cross-pollination from these fields invites new applications of DSTs to LLMs.

---

This blog was originally posted at <https://deep-network.org/2025/09/29/paper-notes-computation-through-neural-population-dynamics-vyas-et-al-2020/>

[^1]: Vyas, S., Golub, M. D., Sussillo, D., & Shenoy, K. V. (2020). Computation Through Neural Population Dynamics. *Annual Review of Neuroscience, 43*, 249–275. <https://doi.org/10.1146/annurev-neuro-092619-094115>
