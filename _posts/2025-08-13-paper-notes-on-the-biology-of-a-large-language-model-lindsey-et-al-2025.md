---
title: "Paper notes: On the Biology of a Large Language Model (Lindsey et al., 2025)"
date: 2025-08-13
permalink: /posts/2025/08/paper-notes-on-the-biology-of-a-large-language-model-lindsey-et-al-2025/
excerpt: "Last week, Deep Network's reading group read *On the Biology of a Large Language Model*. The research team comes from Anthropic's interpretability research group, and was published in the Transformer Circuits interactive research thread as well as on the Anthropic website."
categories:
  - Paper Notes
  - General reading group
tags:
  - artificial intelligence
  - anthropic
  - circuit tracing
  - circuits
  - claude
  - claude-haiku
  - computer science
  - LLM
  - mechanistic interpretability
  - research
  - technology
archive_hidden: true
---

Last week, Deep Network's reading group read *On the Biology of a Large Language Model*.[^1] The research team comes from Anthropic's [interpretability research group](https://www.anthropic.com/research#interpretability), and was published in the [Transformer Circuits](https://transformer-circuits.pub/) interactive research thread as well as on the Anthropic website.

The lead author is [Jack Lindsey](https://jlindsey15.github.io/), whose research interests cross machine learning and neuroscience. "Core contributors" (second authors?) include [Wes Gurnee](https://wesg.me/), with a PhD focused on interpretability and experience with data pipelines, and [Emmanuel Ameisen](https://www.linkedin.com/in/ameisen/), who has extensive applied AI experience.

The paper explores Anthropic's lightweight Claude 3.5 Haiku production model through home-grown circuit tracing tools, which they have [open-sourced](https://www.anthropic.com/research/open-source-circuit-tracing). It reveals computational graphs executed in the model's processing of various test inputs.

## Views on the paper

This was a lively meeting, with opinions about the circuit tracing technology, what it reveals in the models, what it might reveal about the human mind, how it might be used for engineering purposes, and problems preventing its application to frontier engineering. I've presented them in an order which flows naturally.

**Jack:** This paper helped me deeper understand circuit tracing and the behaviour LLMs. I found it interesting in how these patterns of “reasoning” often matched human thought patterns.

**Shetal:** It was super cool to see Anthropic's methodology in interpreting their LLMs, specifically Claude 3.5 Haiku. Amongst other things, we learnt that this model can think diagnostically ("re-reading" prompt to inform final output). I was most fascinated by the circuit tracing tool they used (recently made open source) to create attribution graphs, which we (as humans), can then analyse to make conclusions/run AI thought experiments as was done in the paper.

**Nic:** These fascinating syntactic triggers were so present in poetry and jailbreaks. I expect more nuanced prose dominos in larger models. I wonder if similar graphing and CoT techniques could be applied to humans?

**Stephen:** I see near-future capability improvements coming from technologies like Anthropic's circuit tracing. Gains from scale are plateauing and RL is scattergun and difficult to align. In this paper, we see interpretability being used to reveal cognitive structures inside the model; it follows that they could be used to enhance cognition, perhaps in concert with RL or model editing methods.

**Peter:** I doubt if the next breakthrough in AI will be mechanistic-informed engineering. Even though the premise is sound, there are many questions regarding the nature of AI remaining unresolved. Problems such as polysemanticity or superpositions have not yet had any satisfying solutions, thereby eluding us from understanding and controlling these systems effectively.

---

This blog was originally posted at <https://deep-network.org/2025/08/13/paper-notes-on-the-biology-of-a-large-language-model-lindsey-et-al-2025/>

[^1]: Anthropic. (2025). On the biology of a large language model. Transformer Circuits Thread. <https://transformer-circuits.pub/2025/attribution-graphs/biology.html>
