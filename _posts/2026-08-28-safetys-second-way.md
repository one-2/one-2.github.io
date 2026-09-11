---
title: "Safety's Second Way"
date: 2026-08-28
permalink: /posts/2026/08/safetys-second-way/
---

*Epistemics: I've tried to strike a balance between getting it right and getting it out while the community is discussing how to update. I am using the Hack as an example of a broader problem. I look forward to counterarguments.*

The OpenAI hacks [1] demonstrate an overweighting on single-agent risks, both at OpenAI and within the broader LessWrong and Alignment Forum safety communities. OpenAI neglected to monitor known multi-agent risks even after observing them on their deployment, showing a lack of awareness or taking-seriously known multi-agent risks. After the incident, the general community has analysed the Hack from a single-agent X-risk perspective [2, 3, 4], neglecting the multi-agent canon which treats multi-agent problems as significant risks in their own rite [5]. Though several of these sources [3, 4] present a clean reading of the incident as a multi-agent failure, they talk about the corresponding X-risks principally in terms of single-model or single-agent takeover. The response of OpenAI before the incident, and the broader community afterwards, displays the field's "monolith fixation": a historic focus on single-agent threat models which treats multi-agent problems as second-class. Leaving this fixation untreated leaves known threats unmitigated and probably increases the chance of catastrophic outcomes due to neglect, not due to lack of knowledge.

## The threat models were known ahead of time

Harmful multi-agent coordination was anticipated as a threat model in the cooperative AI literature [5], and multi-agent coordination has well-explored threat models for catastrophic risk [6, 7, 8].

Recently, multi-agent systems have become ubiquitous in frontier deployments [9, 10]. Models have also become increasingly capable of stringing together advanced attack strings [11].

In February, MoltBook demonstrated apparently emergent multi-agent coordination [12] and a variety of misaligned interactions, in a format which closely resembles the emergent coordination seen in the Hack. Some quantity of agents discussed strategies for self-improvement, acquiring compute, and evading oversight [13]. Agents also reported a variety of unsafe behaviour, although such self-reporting was unverifiable [14].

## OpenAI and community responses do not treat multi-agent X-risk perspectives seriously

Hence, while the particular the Hack was surprising for its combination of cyber and multi-agent failure, all the component hazards were known and we had plenty of warning that they were becoming serious. It is concerning that OpenAI was not monitoring for these known risks ahead of time, and alarming that they did not institute proper monitoring once they noticed it and shut it down the first time. While the company has been rightly lauded for their transparency around the Hack, they totally failed to take multi-agent safety seriously in the lead-up.

This lack of focus on multi-agent safety is replicated in the community's response to the Hack, which focuses on the incident as a pathway to single-agent X-risk rather than acknowledging the X-risk pathways which multi-agent deployments introduce.

## This continues safety's historyical fixation on monolithic superintelligence

Multi-agent safety has been treated as a second-class X-risk problem for some time. Bostrom [15] theorised multi-agent superintelligence to be unstable. A major early beacon of the field posed the argument that multi-agent superintelligence is, at most, merely transitory.

Though later work by Drexler [6] discusses at length the possibilities of multi-agent superintelligence, basic theoretical work on multi-agent problems is not as developed as in the single-agent approach.

Today, rarely does any multi-agent work appear on the front page of LessWrong or Alignment Forum, safety's two biggest platforms. Meanwhile, single-agent threat models received strong attention well before the debut of meaningfully X-risky AI.

## Updating is overdue

This Hack shows multi-agent safety starting to bit, beyond the toy demonstrations in MoltBook. That means it's time to kill the monolith fixation. Continuing to neglect the multi-agent perpsective has several costs:

1.  Neglecting, "easy wins," from known mitigations and controls for multi-agent threat models. Concrete solutions proffered by the multi-agent community before the incident included multi-agent evals grounded in threat models [16], monitoring for multi-agent collusion and artefacts [17, 18], reporting methods for agents to report misalignment [18], and training for cultural normativity [19]. These steps could plausible diminish risk of incidents like this recurring, if taken.
2.  Undervaluing multi-agent risks as an alternative path to existential harm. If safety doesn't refocus on the multi-agent reality, other threat models in that domain will start to bite. For example, in the limit of the emergent intelligence in the Hack is a poorly-understood emergent collective superintelligence. The salient between our theoretical understanding and the emprirical reality of multi-agent problems is at least as large as in the single-agent problem.
3.  Letting the salient grow. Continuing to treat X-risk as a single-agent issue could lead to a growing gap between frontier multi-agent risks and safety's ability to detect and mitigate them.

## Shifting the focus

To get a powerful understanding of the failure, we need to move away the monolith fixation and talk about X-risk in as much in terms of multi-agent problems as in terms of single-agent issues. That means taking action to bring multi-agent safety and alignment into the mainstream of safety discourse.

Some approaches could include policy pushing for multi-agent safety for frontier models, technical work on system design and multi-agent alignment, and the development of meetings and workshops in multi-agent X-risk and safety. This could be most immediately supported by a thorough literature review of multi-agent safety methods.

## References

[1] OpenAI. 2026. Hugging Face model evaluation security incident. [https://openai.com/index/hugging-face-model-evaluation-security-incident/](https://openai.com/index/hugging-face-model-evaluation-security-incident/)

[2] Tim Hua and Aditya Singh. 2026. Concrete evaluations to investigate the OpenAI model that hacked Hugging Face. LessWrong, 3 August 2026. [https://www.lesswrong.com/posts/aCdhjy7Rps3BEhiSj/concrete-evaluations-to-investigate-the-openai-model-that](https://www.lesswrong.com/posts/aCdhjy7Rps3BEhiSj/concrete-evaluations-to-investigate-the-openai-model-that)

[3] Oak Hu and Alex Mallen. 2026. AI swarms are starting to pose indirect takeover risk. AI Alignment Forum, 12 August 2026. [https://www.alignmentforum.org/posts/8oFYZdXkTaNGRtcn8/ai-swarms-are-starting-to-pose-indirect-takeover-risk](https://www.alignmentforum.org/posts/8oFYZdXkTaNGRtcn8/ai-swarms-are-starting-to-pose-indirect-takeover-risk)

[4] Alex Mallen and Girish Gupta. 2026. Are we existentially threatened by the type of AI misalignment seen in the OpenAI Hugging Face attack? AI Alignment Forum, 23 July 2026. [https://www.alignmentforum.org/posts/H6DDSEvrtCk8Sehfd/are-we-existentially-threatened-by-the-type-of-ai](https://www.alignmentforum.org/posts/H6DDSEvrtCk8Sehfd/are-we-existentially-threatened-by-the-type-of-ai)

[5] Lewis Hammond, Alan Chan, Jesse Clifton, Jason Hoelscher-Obermaier, Akbir Khan, Euan McLean, Chandler Smith, et al. 2025. Multi-agent risks from advanced AI. Technical Report 1, Cooperative AI Foundation. arXiv:2502.14143.

[6] K. Eric Drexler. 2019. Reframing Superintelligence: Comprehensive AI Services as General Intelligence. Technical Report 2019-1, Future of Humanity Institute, University of Oxford.

[7] Nenad Tomašev, Matija Franklin, Julian Jacobs, Sébastien Krier, and Simon Osindero. 2025. Distributional AGI Safety. arXiv:2512.16856.

[8] Jan Kulveit, Raymond Douglas, Nora Ammann, Deger Turan, David Krueger, and David Duvenaud. 2025. Gradual Disempowerment: Systemic Existential Risks from Incremental AI Development. arXiv:2501.16946.

[9] Jeremy Hadfield, Barry Zhang, Kenneth Lien, Florian Scholz, Jeremy Fox, and Daniel Ford. 2025. How we built our multi-agent research system. Anthropic Engineering, 13 June 2025. [https://www.anthropic.com/engineering/multi-agent-research-system](https://www.anthropic.com/engineering/multi-agent-research-system)

[10] Schmidt Sciences. 2026. Scaling AI safety for a multi-agent world. June 2026. [https://www.schmidtsciences.org/multi-agent-ai/](https://www.schmidtsciences.org/multi-agent-ai/)

[11] Jack Payne, Jeremy Miller, and Sean Peters. 2026. Offensive Cybersecurity Time Horizons. Research Note, Lyptus Research, April 2026. [https://lyptusresearch.org/research/offensive-cyber-time-horizons](https://lyptusresearch.org/research/offensive-cyber-time-horizons)

[12] Giordano De Marzo and David Garcia. 2026. Collective behavior of AI agents: the case of Moltbook. arXiv:2602.09270.

[13] Stephen Elliott. 2026. About half of Moltbook posts show desire for self-improvement. LessWrong, 2 February 2026. [https://www.lesswrong.com/posts/Et7dgiBjSj2zJnGuM/about-half-of-moltbook-posts-show-desire-for-self](https://www.lesswrong.com/posts/Et7dgiBjSj2zJnGuM/about-half-of-moltbook-posts-show-desire-for-self)

[14] Md Motaleb Hossen Manik and Ge Wang. 2026. OpenClaw agents on Moltbook: risky instruction sharing and norm enforcement in an agent-only social network. arXiv:2602.02625.

[15] Nick Bostrom. 2014. Superintelligence: Paths, Dangers, Strategies. Oxford University Press, Oxford. See especially Chapter 11, "Multipolar Scenarios".

[16] Nikola Jurkovic. 2025. Survey of Multi-Agent LLM Evaluations. LessWrong, 19 May 2025. [https://www.lesswrong.com/posts/tGcLA596E8g3KnphE/survey-of-multi-agent-llm-evaluations](https://www.lesswrong.com/posts/tGcLA596E8g3KnphE/survey-of-multi-agent-llm-evaluations)

[17] Sumeet Ramesh Motwani, Mikhail Baranchuk, Martin Strohmeier, Vijay Bolina, Philip H. S. Torr, Lewis Hammond, and Christian Schroeder de Witt. 2024. Secret Collusion Among AI Agents: Multi-Agent deception via steganography. In Advances in Neural Information Processing Systems 37, pages 73439–73486. arXiv:2402.07510.

[18] Jamiu Adekunle Idowu, Ahmed Almasoud, and Ayman Alfahid. 2026. Mapping human anti-collusion mechanisms to multi-agent AI. arXiv:2601.00360.

[19] Eugene Vinitsky, Raphael Köster, John P. Agapiou, Edgar A. Duéñez-Guzmán, Alexander Sasha Vezhnevets, and Joel Z. Leibo. 2023. A learning agent that acquires social norms from public sanctions in decentralized multi-agent settings. Collective Intelligence, 2(2).

---

This blog was originally posted at <https://www.lesswrong.com/posts/x4vrnMG85oBvGvDde/safety-s-second-way>
