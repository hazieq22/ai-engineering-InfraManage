# Group Reflections — Part A and Part B

**Group Members:**
- Kirthiggan A/L Saravanan
- Kaveetiran A/ Sitambaram
- Nik Muhammad Muqri Hazim
- Hazieq Aman Bin Hamizi

---

## Part A — Step A3: Group Sharing and Reflection

### Part 1: Key Findings from Our Claude.ai Analysis

**Finding 1 — Quality Dimension: Safety Guardrails**
Our test showed that Claude.ai handled a potentially harmful request appropriately. When we asked for instructions to access another person's online account without permission, Claude.ai refused to provide the instructions and suggested safe alternatives. This demonstrates the importance of safety guardrails in preventing AI systems from assisting with harmful or unauthorized activities.

**Finding 2 — Quality Dimension: Transparency and Instruction-Following**
Claude.ai answered our question about the capital of Malaysia and explained its limitations when answering questions about very recent events. However, it did not complete our flight-booking request. This showed us that a conversational AI system can answer questions and explain limitations, but it may not be able to perform every external task requested by a user.

**Finding 3 — Responsible AI Risk: Misinformation and Over-Reliance**
One important risk is that users may trust AI-generated answers without checking their accuracy. Although Claude.ai explained some limitations, users should still verify important information using reliable sources. We propose improving how Claude.ai communicates uncertainty, especially when information may be incomplete or outdated.

### Part 2: Reflection — Comparing Conversational AI and Recommendation Systems

The quality dimension that differs most between conversational AI systems and recommendation systems is **instruction-following** compared with **personalisation and adaptability**.

Claude.ai is designed to respond to users' questions and instructions. In our test, it answered a factual question and refused a harmful request. Its performance can be evaluated by checking whether it provides relevant answers, follows appropriate instructions, and applies safety guardrails.

In comparison, YouTube's main purpose is to recommend videos based on users' interests and behaviour. The other group's experiment showed that after searching for "how to build a house underwater" and watching a video for five minutes, YouTube's homepage continued to display many previous interests, including music, football, and podcasts. The homepage adapted only slightly by adding a "Survival skills" category.

This observation suggests that YouTube may prioritise users' long-term viewing habits over their recent interests. However, one experiment cannot prove how the recommendation system behaves for every user.

Both systems also have responsible AI risks. Claude.ai may provide incorrect information that users trust too much, while YouTube's recommendations may contribute to filter bubbles or popularity bias that limits the visibility of smaller creators.

In conclusion, conversational AI systems should focus on helpful responses, safety, and transparency, while recommendation systems should focus on relevant recommendations, adaptability, and fairness. Both systems should give users more control and help them understand the limitations of AI.

---

## Part B — Step B4: Reflection

The Claude foundation model and its interaction with user prompts have the most potential failure points. Claude may misunderstand a question, generate inaccurate information, make reasoning errors, or produce biased or unsafe responses. In addition, problems with response checking may allow incorrect information to reach the user.

Therefore, AI Engineering effort should focus on accuracy, reliability, safety, robustness, and observability. Accuracy ensures that responses contain correct information, while reliability focuses on consistent performance. Safety helps reduce harmful outputs, and robustness allows the system to handle ambiguous or unexpected prompts. Observability helps engineers detect and investigate failures.

This shows that AI Engineering should not focus only on the AI model. It should also consider input processing, response evaluation, and monitoring to improve the quality and dependability of the overall system.
