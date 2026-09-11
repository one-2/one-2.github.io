---
title: "Paper Notes: Emergent Cooperation and Strategy Adaptation in Multi-Agent Systems: An Extended Coevolutionary Theory with LLMs (Zarzà et al., 2023)"
date: 2025-10-31
permalink: /posts/2025/10/paper-notes-emergent-cooperation-and-strategy-adaptation-in-multi-agent-systems-an-extended-coevolutionary-theory-with-llms-zarza-et-al-2023/
excerpt: "Welcome to Paper Notes, where we record our groups’ weekly discussions of innovative papers from across artificial intelligence. On Tuesday the 21st of October, our mathematics reading group read Emergent Cooperation and Strategy Adaptation in Multi-Agent Systems: An Extended Coevolutionary Theory with LLMs, published in MDPI Electronics in 2023. The authors come from a collection of three universities and a lab, across Spain and Germany."
categories:
  - Paper Notes
  - Mathematics reading group
tags:
  - agentic ai
  - agents
  - artificial intelligence
  - chatgpt
  - game theory
  - LLM
  - multi-agent systems
  - research
  - research methods
  - technology
---

Welcome to Paper Notes, where we record our groups’ weekly discussions of innovative papers from across artificial intelligence. On Tuesday the 21st of October, our mathematics reading group read [*Emergent Cooperation and Strategy Adaptation in Multi-Agent Systems: An Extended Coevolutionary Theory with LLMs*](https://www.mdpi.com/2079-9292/12/12/2722),[^1] published in MDPI Electronics in 2023. The authors come from a collection of three universities and a lab, across Spain and Germany.

## The paper's claims

The paper approaches the interesting question of how LLMs can influence cooperation in complex multi-agent systems (MAS). This is extremely timely research, given the sudden proliferation of agentic AI across the economy. The paper's abstract claims that the framework, "offers valuable insights into the interplay between strategic decision making, adaptive learning, and LLM-informed guidance in complex, evolving systems." Unfortunately, we found some execution problems which limit the paper's usefulness.

## Questionable research practices

The paper demonstrates some questionable research practices,[^2] which diminish its scientific value and provide valuable lessons on research writing. First of all, the included mathematics is trivial and inappropriate for the task they are tackling. They re-prove foundational game-theoretic results about Nash equilibria which were established in the 1950s, which could instead have been cited as basic results. In particular, they prove results for simplified two-player games (Theorems 1-2), then simulate a 100-agent networked system, without explaining how the theoretical results apply to this more complex setting. In doing so, the authors have assumed away exactly the difficult complexity which is the central problem of the MAS setting.

We were also left wondering why a gradient-based learning rule was selected when established results in Bayesian structure learning or multi-agent reinforcement learning might provide a more appropriate formalism for network structures changing under uncertain payoffs. The choice is not justified against these alternative options.

Secondly, their formalisms do not match their simulations, leaving us unclear what method the simulations used and how those methods are related to the formal framework. In Sections 3 and 4, the authors describe a gradient-based update rule for the two-player game which does not apply to the discrete cooperate/defect environment they use in their simulations. The authors do not address this gap, acknowledging only that, "the simulation environment used in this study is a simplified representation of real-world systems." This disparity calls into question the paper's claim that the framework extends our understanding of MAS.

Thirdly, the paper makes strong claims, "far-reaching implications for both businesses and society as a whole," but does not demonstrate a practical application of the framework or advantages over alternative theories.

Fourth, supporting analysis of the simulations is limited. The paper provides two similar visualisations of a converged state of the simulation, but does not analyse time-series or game-theoretic measures. It is not clear whether the network metrics used in the paper are standard. The paper does not include comparisons to baseline tests or performance of alternative frameworks. The paper does not justify why they consulted the LLM at intervals of 10,000-33,000 rounds, nor do they provide ablations showing the effects of changing this crucial parameter.

Finally, the simulation code and hyperparameter settings are not published, harming reproducibility and replicability.

## Lessons from the paper

We ought to be careful when picking up, or writing, new literature, in particular assuring ourselves some basic standards are met:

- Read critically, and try to identify and address problems emerging while reading before moving on. Gaps early in the paper can undermine the remainder.
- Include a thorough literature review and comparison to existing methods using standard metrics and baselines.
- Use formalisms to directly support simulations, or instead acknowledge they are distinct and develop them in separate papers.
- Publish full details of method, include code.
- Limit claims about impact of the research to the impact directly demonstrated or strongly implied by the work in the paper itself.
- Be wary of journals with reputations for weak peer review, such as MDPI.

---

This blog was originally posted at <https://deep-network.org/2025/10/31/paper-notes-emergent-cooperation-and-strategy-adaptation-in-multi-agent-systems-an-extended-coevolutionary-theory-with-llms-zarza-et-al-2023/>

[^1]: de Zarzà, I., de Curtò, J., Roig, G., Manzoni, P., & Calafate, C. T. (2023). *Emergent Cooperation and Strategy Adaptation in Multi-Agent Systems: An Extended Coevolutionary Theory with LLMs*. Electronics, 12(12), 2722. <https://doi.org/10.3390/electronics12122722>
[^2]: Schimmack, U. (2015, January 24). *Questionable Research Practices: Definition, detection, and recommendations for better practices*. Replication Index. <https://replicationindex.com/2015/01/24/qrps/>
