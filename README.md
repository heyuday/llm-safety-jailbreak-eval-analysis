# Evaluating and Analyzing LLM Jailbreak Defenses  
*A Practical Exploration of AI Safety Techniques*

This project evaluates the robustness of instruction-tuned language models against jailbreak attacks and implements a layered defense pipeline.

Using **Qwen2.5** and **Qwen3Guard**, I benchmarked:
- The success rate of manual and automated jailbreaks (e.g., GCG, AutoDAN)
- The performance of prompt-level and model-level defenses
- Combined defense strategies through a “Swiss cheese” safety framework

**Goal:** Understand how alignment failures emerge in deployed models and quantify the resilience of current defenses under realistic adversarial conditions.

**Developed as part of** the *Wisconsin AI Safety Initiative (WAISI)*, where I serve as a Technical Scholar and Fundamentals Cohort Lead.

---

### Key Findings
- Prompt-level self-reminders reduced ASR by ~7%.
- Guard models (Qwen3Guard) improved safety by ~20%.
- Perplexity filters caught most gradient-based attacks but failed against semantically coherent ones.
- Circuit breaker concepts highlight future directions for mechanistic alignment.

---

### Why It Matters
Each jailbreak revealed how narrow fine-tuning fails to constrain global model behavior.  
Empirical safety work like this complements theoretical alignment, reinforcing the urgency of developing robust, scalable oversight as models approach AGI-level capabilities.

---

**Author:** [Uday Tyagi](https://www.linkedin.com/in/uday-tyagi)  
**Affiliations:** UW–Madison CS / Cornell M.Eng. (Incoming) / KLA / WAISI  
