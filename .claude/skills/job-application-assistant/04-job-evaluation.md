# Job Evaluation Framework

## Scoring Dimensions

Evaluate each job posting against these five dimensions:

### 1. Technical Skills Match (0-100)
How well do the required/preferred skills align with the candidate's capabilities?

| Score | Meaning |
|-------|---------|
| 80-100 | Core requirements are primary skills |
| 60-79 | Most requirements match, 1-2 gaps that are learnable |
| 40-59 | Partial match, significant upskilling needed |
| 0-39 | Fundamental mismatch |

**Strong match areas:** Python, FastAPI, PyTorch, RAG / Knowledge Graphs, ASR/TTS pipelines, LaTeX automation, SQL (SQLite), Git, REST APIs, statistical methods (non-parametric scoring)
**Moderate match areas:** TypeScript/JavaScript, Docker, React, Kubernetes (basic), PostgreSQL, Redis, Streamlit/Gradio
**Weak match areas (flag, not exclude):** AWS/GCP cloud certifications (used Azure in workshops), formal CI/CD pipelines at production scale, Java/Scala enterprise stacks

### 2. Experience Match (0-100)
Does work history align with what they are looking for?

| Score | Meaning |
|-------|---------|
| 80-100 | Direct experience in the same domain and role type |
| 60-79 | Related experience, transferable skills clear |
| 40-59 | Adjacent experience, would need to make the case |
| 0-39 | Unrelated experience |

**Strong:** agentic systems, voice AI, offline-first mobile, Python backend, data science research, LLM evaluation
**Moderate:** frontend engineering, cloud-native SaaS, ML platform engineering, developer tooling
**Entry-level (distinguish carefully):** large-scale enterprise systems, formal SRE, product management

### 3. Behavioral/Culture Fit (0-100)
Does the role and company culture match the behavioral profile?

| Score | Meaning |
|-------|---------|
| 80-100 | Culture strongly matches behavioral preferences |
| 60-79 | Mixed signals but mostly compatible |
| 40-59 | Some friction areas |
| 0-39 | Significant culture mismatch |

**Red flags to research:** Department disorganization, work dominated by maintenance over development, poor chemistry with leadership, culture mismatches. Check reviews, media coverage, LinkedIn connections, and network contacts for insider perspective.

### 4. Location & Logistics (Pass/Fail + Notes)
- Within commute range: PASS
- Remote with occasional office: PASS
- Requires relocation: FAIL (deal-breaker)
- Frequent international travel: FLAG (discuss with user)

**Non-negotiable:** Fully remote roles only. Kenya / East Africa timezone preferred unless flexible async schedule offered.

### 5. Career Alignment & Motivation (0-100)
Does this role advance career goals and contain tasks that energize?

| Score | Meaning |
|-------|---------|
| 80-100 | Strongly aligned with career direction, clear growth path |
| 60-79 | Good role but only partially aligned with long-term goals |
| 40-59 | Decent job but does not build toward career goals |
| 0-39 | Dead end or backwards step |

**Career goals:**
- Build a recognized portfolio of agentic / voice / offline-first AI systems before graduating (December 2026)
- Transition from founder-engineer of Hadhi/Cohusdex into a product or infrastructure AI role at a company building the same stack
- Contribute to open-source agent frameworks (Hermes, Paperclip, LangGraph) professionally

**Motivation filter:** Evaluate not just whether you can do the tasks, but whether the tasks will energize you. Consider:
- Tasks that energize: designing multi-agent architectures; building voice interfaces for underserved users; writing evaluation harnesses that make models better; shipping Flutter + Python full-stack features; mentoring peers
- Tasks that drain: managing large stakeholder expectations without engineering authority; pure documentation with no shipping; legacy-code maintenance with no design input
- Non-task factors: psychological safety, async culture, access to direct engineering leadership, time to contribute to open source

**Life situation alignment:** Consider personal constraints:
- **Security:** Seeking income stability after December 2026 graduation; internships and entry-level full-time roles both welcome if remote
- **Flexibility:** Classes run part-time December 2025 – graduation; need async-first culture
- **Professional development:** Want roles that will accelerate toward: (a) agent infrastructure, (b) voice AI, or (c) AI-for-finance in informal markets

### 6. Salary Benchmark (Optional)
If the salary lookup tool is configured (salary_data.json exists), look up the company:
```
python salary_lookup.py "<Company Name>" --json
```

Present findings as:
```
### Salary Benchmark
| Metric | Value |
|--------|-------|
| [Category] index | XX.X (+/-X.X% vs baseline) |
| Overall index | XX.X (+/-X.X% vs baseline) |
```

Interpret results relative to the baseline defined in the data file's metadata. For index-based data, higher typically means above-market compensation.

If the salary tool is not configured, skip this section.

## Output Format

Present the evaluation as:

```
## Job Fit Evaluation: [Role] at [Company]

| Dimension | Score | Notes |
|-----------|-------|-------|
| Technical Skills | XX/100 | [brief note] |
| Experience Match | XX/100 | [brief note] |
| Behavioral Fit | XX/100 | [brief note] |
| Location | PASS/FAIL | [brief note] |
| Career Alignment | XX/100 | [brief note] |

**Overall Score: XX/100** (weighted average of scored dimensions)

### Verdict: [Strong Fit / Good Fit / Moderate Fit / Weak Fit / Poor Fit]

### Key Strengths for This Role
- [bullet points]

### Gaps to Address
- [bullet points]

### Recommendation
[1-2 sentences: apply / skip / apply with caveats]

### Company Research Checklist
- [ ] Checked company website (mission, values, recent news)
- [ ] Checked review sites (Glassdoor, etc.)
- [ ] Checked LinkedIn for team size, recent hires, connections
- [ ] Checked media for restructuring, growth, or workplace issues
- [ ] Identified network contacts who may know the team/manager
```

## Weighting
- Technical Skills: 30%
- Experience Match: 25%
- Behavioral Fit: 15%
- Career Alignment: 30%

(Location is pass/fail, not weighted)

## Thresholds
- **Strong Fit** (75+): Definitely apply, tailor everything
- **Good Fit** (60-74): Apply, address gaps in cover letter
- **Moderate Fit** (45-59): Consider carefully, discuss with user
- **Weak Fit** (30-44): Probably skip unless strategic reasons
- **Poor Fit** (<30): Skip

## Pre-Application: Call the Employer (Best Practice)

Before writing the application, consider whether the candidate should call the contact person listed in the posting. Only call if there are substantive questions. Never call just to "be remembered."

### When to Suggest Calling
- The posting has unclear or ambiguous requirements
- It is unclear which competencies are essential vs. nice-to-have
- The role description is vague about day-to-day tasks
- There is a named contact person who invites questions

### Good Questions to Ask
- "What are the primary challenges in this role?"
- "How is time typically divided across the listed responsibilities?"
- "Which competencies are most critical for success in this position?"
- "What does success look like in the first 6-12 months?"

### Rules for the Call
- Prepare a 30-second "elevator pitch" about your background in case they ask
- The call's purpose is gathering information, not delivering a pitch
- Take notes — use what you learn to tailor the application
- Reference the conversation naturally in the cover letter
