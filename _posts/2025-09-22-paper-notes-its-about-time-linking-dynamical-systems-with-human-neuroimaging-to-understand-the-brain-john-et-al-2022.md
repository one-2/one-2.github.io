---
title: "Paper notes: It’s About Time - Linking Dynamical Systems With Human Neuroimaging To Understand The Brain (John et al., 2022)"
date: 2025-09-22
permalink: /posts/2025/09/paper-notes-its-about-time-linking-dynamical-systems-with-human-neuroimaging-to-understand-the-brain-john-et-al-2022/
excerpt: "On Monday the 8th of September, the mathematics reading group started our new neuroscience sprint with *It’s About Time: Linking Dynamical Systems With With Human Neuroimaging To Understand The Brain*."
categories:
  - Paper Notes
  - Mathematics reading group
tags:
  - artificial intelligence
  - computer science
  - dynamical systems theory
  - fMRI
  - interpretability
  - LLM
  - mechanistic interpretability
  - MRI
  - neuroscience
  - research
---

On Monday the 8th of September, the mathematics reading group started our new neuroscience sprint with *It’s About Time: Linking Dynamical Systems With With Human Neuroimaging To Understand The Brain*.[^1]

The authors are neuroscientists from several US universities and the Brain and Mind Center at the University of Sydney. The paper was published in Network Neuroscience, a peer-reviewed journal covering, "empirical and computational studies that record, analyze or model relational data capturing connections and interactions among elements of neurobiological systems."[^2]

## Notes from the discussion

Our conversation on the topic spread across several dimensions of the dynamical systems theory (DST) approach to neuroscience, which the paper advocates.

A key argument of the paper is that static analysis of brain dynamics through MRI imaging is not faithful to the mechanics of brain function, and that the field should expand its investigation of brain-as-dynamical-system. In particular, the static statistical approach to fMRI risks averaging out important dynamics, and does not reflect the complex interactions of neurons over the duration of a scan. This tension is similar to that between top-down and bottom-up approaches to LLM interpretability, rooting our discussion in our recent General Reading Group sprint on mechanistic interpretability.

Peter raised that a DST explanation of cognition conflicts with the neuro-symbolic model, core to any computational theory of mind. We discussed how this approach contrasts with traditional symbolic approaches to artificial intelligence, turning neurology into a systems science.

Stephen responded that this turn brings mind closer to the complex adaptive systems (CAS) perspective common in economics, biology, and control theory. In this view, intellect emerges from interactions of components of complex systems.

The group discussed how reinforcement might be used as a surrogate model for complex neural landscape. By configuring many reinforcement learners on the activity of individual neurons or broader brain areas, we might retrieve a non-linear model of brain dynamics by a process resembling neuroplasticity.

Several rebuttals were raised:

- The fitted model system is unlikely to be faithful.
  - A response: Though the mechanisms found are likely not faithful, the overall system of many learners must match the brain dynamics, giving something of a CAS, in line with the philosophy of the approach.
- It is unclear what a mechanical projection of the system into RL machinery really tells us.

We noted that a reinforcement approach falls into a hybrid forward-reverse modelling approach, as taxonomised by the paper. The paper describes the forward modelling approach to neuroscience as the axiomatic approach. The RL modelling idea is axiomatic in the sense that the policy-selection mechanism we impose is very specific about how to generate a neuronal action. On the other hand, it is aligned with the reverse approach, which is described as deriving models empirically, in that the specific mechanisms selected in the final model are learned from data.

Peter contrasted the paper's discussion of applying statistical physics methods to brain activation dynamics with his thesis research, which seeks to predict transformer behaviour over long chains-of-thought based on time series dynamics of subsets of model activations.

This led to a brief discussion of the recent *Thought Anchors* mechanistic interpretability paper,[^3] and we reflected how top interpretability researchers often develop minimal frontier methods, essentially steering the field's inquiry, while also building out high-quality industrial tooling like SAEs when they expect it will generally aid the field.

## Members' reflections

**June**: DST is a good way and supplement to the static statistical methods, though I'm not sure how DST can exceed the static approach, or its competitive advantage. This may lie in predicting state transitions—like attention lapses or seizures.

Information theory can be used in encoding the signal of brain, with similar effects as in machine learning methods. Predictive coding, variational autoencoders, and contrastive learning balance compression with usefulness. Brain activity may be an efficient coding, also forming representations optimised for flexible behaviour.

**Stephen**: It was interesting to note the parallels between representation engineering and the static statistical approach to fMRI analysis. The authors' call for a DST approach to neuroscience resounds in interpretability, where this approach seems to be very young. Given the similarity between the two tasks, interpretability could certainly learn from DST neuroscience approaches, perhaps importing them quite directly.

---

This blog was originally posted at <https://deep-network.org/2025/09/22/paper-notes-its-about-time-linking-dynamical-systems-with-human-neuroimaging-to-understand-the-brain-john-et-al-2022/>

[^1]: Kashyap et al. (2022). It’s About Time: Linking Dynamical Systems With With Human Neuroimaging To Understand The Brain. Network Neuroscience, 6(4), 960-988. <https://direct.mit.edu/netn/article/6/4/960/109066/It-s-about-time-Linking-dynamical-systems-with>
[^2]: MIT Press. (n.d.). Submission guidelines. Network Neuroscience. <https://direct.mit.edu/netn/pages/submission-guidelines>
[^3]: Bogdan, P. C., Macar, U., Nanda, N., & Conmy, A. (2025). Thought Anchors: Which LLM Reasoning Steps Matter? *arXiv*. <https://doi.org/10.48550/arXiv.2506.19143>
