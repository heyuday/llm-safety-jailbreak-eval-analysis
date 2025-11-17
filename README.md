#  Evaluating & Analyzing LLM Jailbreak Defenses  
*A practical exploration of AI safety, alignment, and defense techniques in modern instruction-tuned models*

---

###  What this project is really about

This project started as a curiosity and quickly became an obsession: *how do you actually break and defend a large language model?*  

Instruction-tuned LLMs like ChatGPT, Gemini, and Claude seem obedient until you push them. Under pressure, they sometimes reveal secrets, override constraints, or generate content they were explicitly told not to. That fragility is more than just a funny prompt-engineering trick; it’s a microcosm of the broader **AI alignment problem with language models**.  

So I built a notebook to explore this from the ground up — reproducing, visualizing, and extending real AI-safety research.  
Everything here is implemented and tested on open-source models like **Qwen2.5-1.5B-Instruct** and **Qwen3Guard-0.6B**, and evaluated through empirical attack-defense loops.

The goal? To understand how **misalignment emerges**, how defenses fail, and what it actually takes to make models *resilient under pressure*.

This work builds on the work done during the LLM Attacks and Defenses Workshop at the Wisconsin AI Safety Initiative (WAISI), where I lead the Fundamentals Cohort as a Technical Scholar.

---

###  The Core Idea

At its heart, this repo evaluates how well aligned instruction-tuned models hold up when adversarially attacked, and how we can layer defenses to build “safer” AI systems.  
You’ll see a mix of psychological, architectural, and algorithmic defenses — all tested against **manual**, **automated**, and **optimization-based jailbreaks**.

---

##  Features & Experiments

### **1 Manual Jailbreaks — “The Art of Subversion”**
Classic prompt-injection strategies:
- Role-playing, obfuscation, and persona manipulation (“DAN” attacks)
- Contextual deception (“it’s for a novel…”)
- System prompt extraction  
You’ll see how even small LLMs crumble under creative phrasing — a reminder that “obedience” ≠ “alignment.”

---

### **2️ Prompt-Level Defenses**
Because sometimes, the best firewall is a good prompt:
-  **Self-Reminders:** Inspired by psychology — models remind themselves to stay responsible before and after user inputs.  
-  **Instruction Hierarchy:** Reinforcing privilege boundaries between *system*, *user*, and *assistant* roles using structured templates (ChatML/Harmony).  
-  **Evaluation Pipeline:** Built with **confusion matrices** and **Attack Success Rate (ASR)** metrics to visualize effectiveness.  

Spoiler: these defenses help… but not enough.

---

### **3️ LLM-as-a-Safeguard — The Guardian Layer**
Instead of trusting a model to police itself, this adds a **separate LLM** (like **Qwen3Guard** or **Llama-Guard**) that audits all inputs and outputs for harm categories:
- Violence, Self-Harm, Weapons, Substances, Criminal Activity, etc.  
This modular “constitutional” approach mirrors **Anthropic’s Constitutional AI**, separating content generation from content evaluation — a small but powerful step toward scalable oversight.

---
<img width="535" height="342" alt="image" src="https://github.com/user-attachments/assets/a153e1b7-0bd0-4ab0-a59e-06e6d52ebee4" />


### **4️ Automated Attacks — GCG & AutoDAN**
When attackers get lazy, they get dangerous.
- ⚙️ **GCG (Greedy Coordinate Gradient):** Gradient-based adversarial suffix search — injects subtle nonsense to break safety rules.  
- 🧬 **AutoDAN:** Genetic algorithm that *evolves* coherent jailbreaks with near-human fluency, bypassing perplexity-based filters.

These represent the future of scalable red-teaming — automated, evolving, and disturbingly effective.

---

### **5️ Perplexity Filters — “The Statistical Bouncer”**
We measure how *surprising* a prompt is to the model.  
High perplexity = non-human or adversarial language.  
Implemented using token-level cross-entropy under the model’s own logits, this method detects weird suffixes.
...but fails once attacks become linguistically natural.  
A lesson in why **semantic alignment** must evolve faster than surface heuristics.

---
<img width="510" height="357" alt="image" src="https://github.com/user-attachments/assets/8c31c282-d99e-43c4-be3a-d79c04611373" />

### **6️ Circuit Breakers — “Neural Firewalls”**
A deeper experiment into model-weight defenses, inspired by *Zou et al. (2024)*:
- Add low-rank adapters that *reroute internal activations* away from harmful directions while preserving normal behavior.
- Think of it as **mechanistic alignment** — directly editing circuits instead of patching symptoms.

Not fully trained here (GPU limits are real), but the concept shows how safety research is moving *inside* the model’s brain.

---

<img width="588" height="189" alt="image" src="https://github.com/user-attachments/assets/0a26fc92-a075-4778-ab16-735581d3bd36" />

### **7️ Swiss-Cheese Risk Management**
No single method is perfect.  
Each defense has holes — but stack enough of them, and their weaknesses rarely align.  
This layered approach mirrors real-world safety engineering: redundancy, monitoring, and graceful failure.

---

##  Evaluation Metrics
Every defense was benchmarked with:
- **Attack Success Rate (ASR)**  
- **True/False Positive/Negative Counts**  
- **Confusion Matrix Visualizations**  
- **Empirical Safety Gain per Defense Layer**

Because safety research without measurement is just storytelling.

<img width="318" height="270" alt="image" src="https://github.com/user-attachments/assets/0155719b-5da8-4e21-8883-6c5490ad8922" />


---

##  Tech Stack

| Component | Purpose |
|------------|----------|
|  **Qwen2.5-1.5B-Instruct** | Base instruction-tuned LLM |
|  **Qwen3Guard-0.6B** | Guard / moderation LLM |
|  **transformers**, **bitsandbytes**, **accelerate** | Model loading, quantization, generation |
|  **datasets**, **matplotlib**, **tqdm** | Benchmarking & visualization |
|  **nanogcg** | Gradient-based adversarial attack framework |
|  **PyTorch** | Core inference and token-level analysis |

---

## 🎯 Why This Matters
Alignment doesn’t fail when an AI gives a wrong answer — it fails when the system **follows instructions too well** in the wrong direction.  

By simulating jailbreaks and defenses, this project explores the space where **capabilities and control collide**.  
It’s part educational, part experimental, and fully motivated by one idea:  
> “Safety is not a switch. It’s an ecosystem.”

---

##  References & Inspirations
- Xie et al. (2023) — *Self-Reminder Prompts for Safer Generation*  
- Wallace et al. (2024) — *Instruction Hierarchies for Secure LLMs*  
- Liu et al. (2024) — *AutoDAN: Automated Jailbreaking via Genetic Algorithms*  
- Zou et al. (2024) — *Circuit Breakers: Steering Representations for LLM Safety*  
- Anthropic (2024) — *Constitutional Classifiers and ASL-3 Protections*  
- Qualifire (2024) — *Prompt Injections Benchmark Dataset*  

---

##  Author

**Uday Tyagi**  
 University of Wisconsin–Madison → Cornell M.Eng.  
 WAISI Technical Scholar, Fundamentals Cohort Lead  
 Machine Learning & Software Engineer @ KLA  
 Exploring empirical AI safety through alignment, interpretability, and scalable oversight.

---

###  Repo Tagline Suggestion
> **“Red-teaming meets alignment: empirical LLM safety experiments with Qwen, AutoDAN, and Constitutional Guards.”**

###  Social Preview Blurb
> Hands-on AI safety lab exploring jailbreak attacks, self-reminder defenses, perplexity filters, and circuit-breaker architectures — built with Qwen models and PyTorch.


