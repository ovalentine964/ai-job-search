# Interview Preparation Guide

## STAR Format
Structure answers as: **Situation** (context), **Task** (your responsibility), **Action** (what you did), **Result** (outcome).

Keep answers to 1–2 minutes. Be specific. End with what you learned or would do differently.

---

## Ready-Made STAR Examples (From Actual Experience)

### 1. Hadhi Voice-CFO Advisor — Demonstrates: agentic AI architecture, real-user evaluation, non-parametric methods
**S:** Informal-market traders in rural Kenya had no formal credit history and no access to financial summarization tools in their mother tongue (Luo). I wanted to validate whether an offline-first agentic system could produce credit-scoring signals that banks could trust.
**T:** Design and pilot a Sigma_1R non-parametric scoring method across 500 traders while keeping the entire stack offline-first (≤2GB RAM mobile) and voice-driven (Luo ASR/TTS).
**A:** Built the 5-agent OpenClaw Hermes pipeline (Ear → Linguist → Bookkeeper → Statistician → Advisor) backed by a Knowledge Graph; evaluated collection quality against a 20% labelled ground-truth sub-sample and refined scoring buckets to reduce false-negative rate.
**R:** Achieved 71% accuracy on the pilot dataset; the output signals were sufficient to generate structured credit reports for a partner bank's thin-file scoring stage.
**Use for:** "Walk me through your biggest technical risk and how you de-risked it", "How do you balance research rigor with shipping deadlines?"

### 2. Sigma_1R — Demonstrates: statistical innovation, hackathon delivery, non-parametric reasoning
**S:** Standard parametric credit-scoring methods rely on large labelled datasets that do not exist for informal-market borrowers. At the Databricks Gen AI Hackathon, I wanted to produce a method that worked on 500 samples.
**T:** Deliver a tested non-parametric scoring method within 48 hours that generalizes across thin-file cohorts.
**A:** Defined Sigma_1R by combining distribution-free hypothesis testing with a similarity-to-peer centroid metric; implemented in Python with pytest; iterated on 3 versions based on mock-environment feedback.
**R:** Named Global Top 5 Finalist (Non-US) out of 500+ submissions; approach now forms the statistical backbone of Hadhi.
**Use for:** "Tell me about a time you had to solve a problem without precedent", "Walk me through a technical decision you made under time pressure"

### 3. NeurIPS Submission — Demonstrates: research-to-production pipeline, evaluation rigour, collaboration
**S:** Existing evaluation pipelines for agentic LLMs produced noisy, irreproducible signals. As a research assistant, I needed to contribute an evaluation framework that the community could run and extend.
**T:** Design and validate a practical evaluation harness within a 12-week research window.
**A:** Built a WebSearch-based evaluation pipeline integrated into an lm-eval-harness fork; designed 4 benchmark tasks targeting grounded reasoning; ran 3× trials per model; contributed code and analysis to the paper.
**R:** Co-authored an AI4Science Workshop paper at **NeurIPS 2025**; contributed open-source evaluation tasks that the harness community merged upstream.
**Use for:** "How do you evaluate whether a model is actually working?", "Tell me about a paper you are proud of"

### 4. Pathway Predictor GNN — Demonstrates: model-building, rapid upskill, measurable impact
**S:** The biology research group spent 6 hours per prediction run using manual feature engineering. I wanted to see whether a graph neural network could replace that workflow.
**T:** Build, train, and validate a GNN metabolic pathway predictor in 12 weeks using real lab data.
**A:** Taught myself PyTorch Geometric over a weekend, then implemented a variant of a Graph Attention Network; set up a data-preprocessing pipeline in PyTorch that normalized SMILES strings and computed molecular graph features; cross-validated on the group's labelled dataset.
**R:** Reduced prediction error by 60% versus the manual baseline; the group adopted the model as its standard tool for the rest of the year.
**Use for:** "Tell me about a complex technical project you owned", "How do you learn new frameworks quickly?"

### 5. Skill Assessment Platform — Demonstrates: full-stack delivery, mentorship, stakeholder communication
**S:** 400+ CS students at MMUST had no consolidated, self-paced way to assess their readiness across networking, OS, and databases. Lecturers manually graded paper quizzes.
**T:** Ship a self-service skill-assessment tool within a semester.
**A:** Built a Django backend with a Vue.js frontend; designed 120+ auto-graded questions across 6 modules; synced results to a lecturer dashboard; mentored 2 junior contributors through the first release.
**R:** Served 400+ students in the first semester; the platform is still in active use at MMUST.
**Use for:** "Tell me about a product you built from scratch", "How do you handle user feedback?"

### 6. OpenCLaw Hermes / Paperclip contribution — Demonstrates: systems design, library contribution, community engineering
**S:** While building Hadhi, I needed an agent runtime that could run inside 2GB of RAM on a mobile device and still support multi-step tool use. Existing frameworks were too heavy.
**T:** Extend the Paperclip/OpenClaw stack to support the Ear → Linguist → Bookkeeper → Statistician → Advisor pipeline on a resource-constrained device.
**A:** Designed the 5-node pipeline contract, wrote 20+ engineering documents defining the interface standards, contributed evaluation code upstream, and maintained an open-source fork under the Cohusdex GitHub organization.
**R:** The runtime now drives Hadhi end-to-end; the design documents have been incorporated as reference architecture by 3 related open-source projects.
**Use for:** "Tell me about a time you had to design from first principles", "How do you contribute to open-source projects?"

---

## Common Tough Questions

### "You are a final-year student with limited full-time experience. Why should we hire you over someone with more experience?"
> Frame this around learning velocity and ownership. My record is: in 18 months I shipped a NeurIPS paper, a Databricks finalist project, a Flutter mobile app, and an open-source framework contribution, all while studying full-time. I learn frameworks over weekends and ship them by Monday. A more senior hire might expect a month of onboarding before producing; I expect to produce on day one because I have already done the equivalent work as a solo project lead.

### "Your project Hadhi sounds like a startup. Are you sure you are ready to join a structured engineering team?"
> Yes, because Hadhi is deliberately built with the same code-review, documentation, and testing culture I would bring into any team. I lead a Swarm Team of 8 sub-agents (Athena, Da Vinci, Turing, Euler, etc.) and assign architecture reviews to Socrates — I designed that role myself because I value having a second opinion before merging. I am used to structured processes, I invent them when none exist.

### "Why did you leave / not pursue [alternative path]?"
> Be honest and forward-looking. "I chose to apply here because [specific company/role/mission] aligns with [specific goal]. I am not running from something, I am running toward this."

### "You don't have [specific skill/experience]."
> Acknowledge the gap, bridge to adjacent experience, show willingness to learn. "I have not used [X] in production, but I used [adjacent skill] in [project] where [similar problem]. I am already reading [official docs / course] and will be productive within 2 weeks."

### "Where do you see yourself in 5 years?"
> Show ambition aligned with the role's growth path. "In 5 years I want to be a lead engineer or technical product manager building voice-first or agentic systems that serve 1M+ users in Africa or similar markets. This role at [company] is the best stepping stone because [specific reason]."

### "What's your biggest weakness?"
> Genuine weakness with concrete mitigation strategy. "I sometimes over-extend on the initial architecture and need an explicit 'timebox' to force a prototype. I now write a 1-page 'must-have vs. nice-to-have' spec before any new component to keep scope in check."

### "Why this company specifically?"
> Customize per company. Must reference: specific products, engineering blog posts, mission statements, recent launches, market position, or team structure. Never give a generic answer.

---

## Questions You Should Ask Interviewers

### About the Role
- "What does a typical week look like in this role?"
- "What would success look like in the first 6 months?"
- "What is the biggest technical challenge the team is facing right now?"

### About the Team
- "How big is the team, and how do you divide ownership across components?"
- "What does the development lifecycle look like, from idea to production?"
- "How does a new engineer onboard? Is there a structured mentorship program?"

### About Tech & Growth
- "What is your current stack for [AI platform / voice infrastructure / mobile]?"
- "Is there room to grow into more architectural or technical-lead decisions?"
- "How does the team stay current with agent frameworks and LLM tooling?"

### About Culture (prevent disappointment)
- "How would you describe the team culture in one sentence?"
- "What does professional development look like here?"
- "Is there flexibility for remote / async-first work?"
- "What is the balance between new features and maintenance?"
- "How would you describe the engineering leadership style?"
- "What do people who thrive here have in common?"

---

## Phone/Video Interview Tips
- Have STAR examples written out (use this file)
- Keep a glass of water nearby
- Smile when speaking (it changes your tone on video)
- Ask for clarification if a question is vague
- Is it OK to take 5 seconds to think before answering
- End with: "Is there anything else you would like to know about my background?"

---

## After Application (Best Practice)

### Follow-Up Etiquette
- Do not call to "stand out" or learn more post-submission unless genuinely necessary
- Respect employer-specified timelines
- If 2+ weeks pass with no update and no timeline was given, a brief status-check call is acceptable
- If you have genuinely new relevant information (e.g. a poster acceptance or new project launch), a short update is fine

### Thank-You Notes
- After any positive update (interview, offer, even a rejection with useful feedback), send a brief thank-you
- Express appreciation for their time and the process
- Keep to 2–3 sentences

---

## Roleplay Guidelines
When doing mock interview practice:
1. Ask which role/company to simulate
2. Start with easy warm-up questions ("Tell me about yourself")
3. Progress to role-specific technical questions
4. Include 1–2 behavioral questions using competencies from the job posting
5. End with a tough question or curveball
6. After each answer: brief feedback on what worked, what to sharpen
7. Suggest which STAR example from this file would work best
