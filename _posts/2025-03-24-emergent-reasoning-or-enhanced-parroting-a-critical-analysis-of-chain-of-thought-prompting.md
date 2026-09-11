---
title: "Paper notes: Chain-of-Thought Prompting Elicits Reasoning in Large Language Models (Wei et al., 2022)"
date: 2025-03-24
permalink: /posts/2025/03/emergent-reasoning-or-enhanced-parroting-a-critical-analysis-of-chain-of-thought-prompting/
excerpt: "A critical analysis of Google's 2022 paper on Chain of Thought Prompting, discussing interesting results, methodological questions, and implications."
categories:
  - Critical Analysis
tags:
  - artificial intelligence
  - chain of thought
  - computer science
  - LLM
  - methodology
  - reasoning
  - research
  - science
archive_hidden: true
---

## Introduction

In 2022, a Google research team published a paper called *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models*, showing that inserting explicit reasoning steps into few-shot exemplars significantly improves large language models’ performance on multi-step reasoning tasks. The paper presents chain-of-thought (CoT) prompting as a method to improve LLM performance, demonstrating state-of-the-art improvements in arithmetic, logical, and symbolic reasoning tasks – without architectural modifications or fine-tuning.

This article critically examines the paper’s claims, assumptions, and implications. We summarise the paper, draw out its interesting contributions, and critique some methodological holes.

We discuss some interesting questions from our reading group session on the paper.

- Does CoT activate reasoning structures in the model, as Google famously claimed (“Language Models Perform Reasoning via Chain of Thought” [blog post](https://research.google/blog/language-models-perform-reasoning-via-chain-of-thought/))?
- Or does CoT simply nudge the model into retrieving chains-of-thought that the model saw in its training data?
- Why does CoT help performance in 100B+ parameter models, but hurt performance in smaller models?
- What does CoT reveal about how LLMs store and retrieve structured knowledge?
- Why is CoT robust to the choice of exemplar annotator, but suffers under shorter reasoning chains?

We answer these where we can, highlight open questions, and point out directions for further research in this area. Some of these have been profitably pursued since the paper’s 2022 publication, including training reasoning structures directly into the models and training on formal languages.

The ideas presented in this paper were developed in conversation with Patrick, Ahnaf, and Joey, over two reading group sessions of the new Deep Network student research group at UNSW, Sydney. Patrick reviewed a draft of the paper. Thank you all for your contributions.

## Contents
{: .no_toc}

* Contents
{:toc}

## Definitions

Before discussing the paper, we define some relevant terms:

- Chain-of-Thought (CoT) Prompting: A prompting strategy for language models where explicit reasoning steps are inserted into examples provided in the prompt, encouraging models to generate structured reasoning responses at inference time.
- In-context Learning: The ability of a model to perform new tasks by conditioning on examples included within the prompt itself, rather than by changing the weights (by fine-tuning or external training updates).
- Emergent Reasoning: The hypothesis that reasoning abilities spontaneously appear in large language models as their parameter count crosses certain thresholds, without explicit programming for logical inference.
- Few-shot Learning: Learning a new task from a limited number of labelled examples provided directly within the prompt.
- Zero-shot Learning: Learning a new task from instructions alone, without any labelled examples in the prompt.
- Ablation Studies: Experiments designed to test which components of an experimental intervention (e.g., prompting method) are necessary for observed improvements. Ablations isolate specific causal factors by systematically removing or altering individual components.

## The Paper

### Method

The authors present CoT prompting as a method to improve structured problem-solving by inserting reasoning steps into few-shot exemplars. If effective, it would have several advantages:

1. It allows dynamically allocating compute time to more challenging problems;
2. It provides an interpretable window into the model’s processing structures;
3. It can be used in any language-based task;
4. It operates at inference time, allowing it to work with any large off-the-shelf foundation model without expensive fine-tuning.

### Results

The authors find that CoT prompting dramatically improves foundation model (LaMDA 137B, PaLM 540B, and GPT-3) performance on established LLM reasoning testbeds:

- Maths word problems (GSM8K, SVAMP, and MAWPS datasets);
- Commonsense reasoning (CSQA, StrategyQA, Date, Sports, SayCan datasets); and
- Symbolic reasoning (letter concatenation and coin flip datasets, both in and out-of-domain).

These results are copied in the figures below.

![Figure 4 from Wei et al. (2022): solve rates on GSM8K, SVAMP, and MAWPS for LaMDA, GPT, and PaLM across model scales, comparing standard prompting, chain-of-thought prompting, and the prior supervised best.](/images/posts/2025-03-chain-of-thought/fig4-math-word-problems.png) ![Figure 8 from Wei et al. (2022): solve rates on letter concatenation and coin flip tasks, in domain and out of domain, for standard and chain-of-thought prompting across model scales.](/images/posts/2025-03-chain-of-thought/fig8-symbolic-reasoning.png)

![Figure 7 from Wei et al. (2022): PaLM solve rates on CSQA, StrategyQA, Date, Sports, and SayCan across model scales, comparing standard prompting, chain of thought, prior supervised best, and human performance.](/images/posts/2025-03-chain-of-thought/fig7-commonsense-reasoning.png)

### Ablation studies

Ablation studies are designed to analyse the effect of sub-components of complex experimental interventions on models’ performance characteristics. The experimenters set up a series of experimental controls, wherein alternative explanations for the model’s changing performance are explored. By refuting alternative explanations for the model’s improved performance, the experimenters evidence a, “process of elimination,” which identifies some part of their experimental intervention as responsible for the change in performance characteristics they observe in their results.

To deduce the cause behind the success of the chain-of-thought method, the authors run several ablation studies:

1. There are no CoT steps in the exemplars (the experimental control);
2. “The model is prompted to output only a mathematical equation before giving the answer”;
3. “The model is prompted to output a sequence of dots (. . .) equal to the number of characters in the equation needed to solve the problem,” the equal-compute ablation; and when
4. The few-shot exemplars contain the chain-of-thought after the answer, instead of before.

These results are copied below.

![Figure 5 from Wei et al. (2022): GSM8K solve rates for LaMDA 137B and PaLM 540B under standard prompting, equation only, variable compute only, reasoning after answer, and chain-of-thought prompting.](/images/posts/2025-03-chain-of-thought/fig5-ablation-study.png){: .align-center}

The authors implicitly hypothesise that CoT prompting improves reasoning performance because it induces the models to reason logically. That is, to somehow compute logical functions of concepts, and, “think through,” problems to solve them, much as humans do. Hence, they structure their ablation studies to identify the relationship between the models' logical reasoning performance and the reasoning component of the CoT technique.

Their ablation studies are strong evidence that mathematical equations in CoT exemplars are not responsible for the CoT method’s benchmark improvements. Models prompted to merely include mathematical equations in their responses do not perform better than the control. Similarly, the authors show that prompting models to include the reasoning chains after providing the answer to the problem cannot be responsible for CoT’s improvements.

### **Methodological flaw in the ablation studies**

The authors claim to successfully refute variable compute as a contributing factor (p. 6), but their ablation does not seem to directly address this variable. The authors claim that Ablation, listed above, causes the model to increase the token count it expends on the answer, thus, “isolat[ing] the effect of variable computation from chain-of-thought reasoning.”

However, for effective identification of the effect of variable compute, it would be necessary to increase compute to a level (approximately) equal to the compute used by the CoT-prompted model on the same task. Reviewing the quoted prompt for Ablation 2 above, it is unclear how the model will behave when conditioned on this prompt. On deeper analysis of this ablation, several flaws emerge.

First, it was known at the time of publication that LLMs could not accurately compute the length of prompted sequences (reference). Then, it seems unlikely that the model will respond to the prompt accurately, returning the number of characters required to solve the problem.

Second, even if models were able to track sequence length internally, it is not clear that the models in question have that capability. None of the foundation models tested were deliberately trained to anticipate the number of characters it will take to solve a problem, and there is no obvious reason to expect they should be able to.

Finally, the ablation seems to contain a logical contradiction. If the model knows how many characters its answer should take, does it not already know the answer? Perhaps the authors are assuming that the model will draw an approximate value of tokens based on similar problems. If such a convergence assumption is made, it should be stated, so that the paper’s conclusions can be interpreted.

Unfortunately, the authors did not report token count or other compute statistics for any of their methods. They also did not report any measure of whether the prompted ablation token lengths were convergent to the token lengths used in correct solutions.

Due to the flawed equal-compute ablation test, the cause of observed performance improvements is not identified as being related to the content of the few-shot exemplars. The results are still consistent with increased compute amount being responsible. Further work is needed to identify the effects of extra compute length and exemplar style on model performance, before deeper conclusions can be drawn about this prompting method.

Nonetheless, further ablation studies show that the technique is robust to different annotators, annotation style, and exemplar source material, which is impressive for practically applying CoT in LLM pipelines. These results are copied below.

![Figure 6 from Wei et al. (2022): GSM8K and MAWPS solve rates for standard prompting and chain-of-thought prompting with different annotators, an intentionally concise style, and exemplars drawn from GSM8K.](/images/posts/2025-03-chain-of-thought/fig6-annotator-robustness.png){: .align-center}

## The Authors’ Interpretation

The authors do not venture why the CoT strategy works, instead focusing on the emergent nature of CoT reasoning improvements. Observing that CoT only helps reasoning performance in models of greater than 100bn parameters, they note that:

1. “Small language models fail at even relatively easy symbol mapping tasks;”
2. “Small language models seem to have inherently weaker arithmetic abilities;” and
3. “Qualitatively... [in our experiments] small language models often did not generate a final answer that could be parsed;”

concluding that, “the success of chain-of-thought reasoning as a result of model scale is a complicated phenomena that likely involves a variety of emergent abilities.” (p16) The authors thereby limit the scope of the paper to reporting their discovery and referencing some suggestive research for future investigation.

Perhaps this is good experimental practice in business: their experiments are limited to what is required to advance the state of the art, and they provide extensive code and suggestion for external researchers to continue investigating the causal mechanisms.

## Our Interpretation

Our reading group’s discussions concluded that the CoT method makes better use of the weights than standard prompting when applied to reasoning tasks, and we see a corresponding performance improvement. We believe this improvement comes from the sequential dependence in the token generation process.

Mimicking the CoT exemplars in its response, the model starts generating words resembling a thought pattern. Then, it, "feeds off itself," providing finer and finer context for the next tokens, like a, “self-guided search process,” in high-dimensional activation space. With increased information density in the context, generation becomes ever more tightly conditioned, creating more targeted or coherent activations dynamics. As evidence, we refer to the CoT-after-answer ablation study. This study showed no performance gain, reinforcing the idea that reasoning must precede an answer to be useful, and lending credence to this autoregressive, or self-conditioning, interpretation.

This interpretation permits both a generalised reasoning and a stochastic parroting explanation for performance improvements, which we discuss in the next section.

## CoT And Generalised Reasoning

The paper does not establish whether the models are reasoning in a generalisable way. An impressive contribution would be to distinguish whether CoT improves generalised reasoning ability, or is merely causing higher-resolution parroting of the training data.

This distinction matters: if CoT is just parroting, then its effectiveness depends entirely on the structured reasoning content of the training data. A parroting interpretation would have critical implications for fields including data quality, fine-tuning, distillation, AI safety, interpretability, and edge (small-model) deployments.

The, “just-parroting,” theory is somewhat evidenced by the paper’s finding that CoT prompting is only effective in models of >100B parameters. Smaller models may lack enough internal structure to reconstruct reasoning chains effectively, making them worse with CoT despite benefiting from traditional few-shot learning. This is reinforced by the results below, which show that scaling PaLM from the 63B to the 540B distilled model reduces both semantic (comprehension) and logical errors.

![Figure 9 from Wei et al. (2022): error analysis of 45 problems that PaLM 62B got wrong, split into semantic understanding, one step missing, and other errors, with the share fixed by scaling to 540B.](/images/posts/2025-03-chain-of-thought/fig9-error-analysis.png)

### CoT does not imply true reasoning

The credibility of the parroting theory fits into a bigger picture: CoT prompting results are not hard evidence of LLMs performing logical reasoning. They merely show an association between reasoning-like inputs and improved model performance on benchmarks.

In the parroting interpretation, CoT introduces a prompt containing structured multi-step response exemplars, the model’s serial dependence causes it to remain in a reasoning-focused generation mode.

This does not require an underlying reasoning ability – only a bias toward generating structured outputs when prompted in a certain way. The associated improvements to reasoning benchmark performance could just be due to higher-resolution (better conditioned) parroting. Without clearer experimental evidence, the paper’s results are consistent with CoT being a well-calibrated retrieval strategy rather than a sign of emergent reasoning.

### **Reasoning as a continuum**

However, if CoT can activate reasoning patterns which were seen in one part of the training data and apply it to different topics (“mixing” reasoning patterns across domains), this suggests that LLMs contain emergent computational properties beyond statistical pattern matching. This would be much closer to the sort of dynamic reasoning in human thought.

Then LLM reasoning may be a continuum: between parroting reasoning structures in-domain; and mixing reasoning patterns across domains. Mixing reasoning structures is an exciting concept, and perhaps heading in the direction of real machine creativity. Even if we limit our ambition to mere in-domain parroting, there is nonetheless great potential to improve LLM performance on explicitly trainable (supervised) tasks.

### **Small models aren’t over**

Our third conclusion is that though improvements from CoT are emergent in large models, this does not mean small models are incapable of reasoning. Refined training procedures might efficiently train reasoning structures into their weights. Targeted optimisation could push small models with sparse or incoherent reasoning structures to behave more like ultra-large models, which memorise weaker reasoning signals simply by virtue of over-parameterisation.

### **Model reasoning chains are not necessarily interpretable**

Our final conclusion is that chains of thought generated by models are not necessarily human-interpretable. Though the model generates reasoning chains, and benchmark results improve, these tokens are a mechanical artefact of the model’s generation process.

It is unclear whether they should cohere with human reasoning structures or expectations. We are tempted to say that they should, as they have emerged from training on web and supervised data. Nonetheless, coherence is not guaranteed or obvious.

## Challenges and Open Questions

The group discussed many questions and challenges related to this paper. We leave these as open questions to spark the curiosity of the audience and members.

- Do large models use their weights efficiently for reasoning, or is significant redundancy present?
- Why does shorter, more concise reasoning in exemplars weaken CoT’s effectiveness?
- Can we jointly train models to reason and produce interpretable reasoning chains?
- Where in the model's weight space does reasoning emerge, and how can we measure or visualise it?
- How has model reasoning capability evolved from 2022 to now, and what architectural or training changes influenced this evolution?
- How can we quantify CoT's computational efficiency across models?
- Are model reasoning errors interpretable in human epistemological terms, such as logical fallacies or cognitive biases?
- How can reasoning errors be mitigated or corrected during inference?

## Alternative Approaches to Improving Reasoning

While CoT is effective, participants noted several other ways to improve structured reasoning. Some have become popular and effective since 2022, when this paper was published.

- Directly encoding domain knowledge: Training models directly on elementary algorithms, such as algorithms for multiplication or spelling that we teach to children.
- External solvers: Attach LLMs to tools, such as programmatic calculators, to handle structured problems. This may be a cheap and practical approach, but it is besides the point of building effective reasoning machines.
- Reinforcement learning: Instead of relying on emergent reasoning, reinforcement learning can be used to train thinking in formally verifiable subjects.
- Verifier-based approaches: Use secondary models to assess reasoning correctness. This introduces the problem of what to do when a verifier rejects a response, so it doesn’t address the reasoning problem. It is nonetheless a useful related tool.

## Conclusion

Chain-of-thought prompting represents a significant advance in the performance of large language models on structured reasoning tasks. While impressive, the original paper’s methodology does not definitively establish that emergent reasoning is occurring in these models, leaving open alternative explanations such as enhanced parroting or self-conditioning during token generation. Our analysis highlighted important methodological weaknesses, particularly in the equal-compute ablation, which leaves room for further experimentation. Whether CoT prompting activates generalised reasoning or improves parroting remains an open question.

## Bibliography

Wei et al. (2023). *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models*. arXiv:2201.11903. Retrieved from <https://arxiv.org/abs/2201.11903>

---

This blog was originally posted at <https://deep-network.org/2025/03/24/emergent-reasoning-or-enhanced-parroting-a-critical-analysis-of-chain-of-thought-prompting/>
