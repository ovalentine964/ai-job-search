# CV Templates and Tailoring Guide

## Template: LaTeX moderncv (Banking Style)

All CVs use the moderncv LaTeX package with the "banking" style and "blue" color scheme.

**Output file:** `cv/main_<company>.tex`
**Compile with:** `lualatex` on TeX Live/MiKTeX. pdflatex often fails with fontawesome5 font-expansion errors; lualatex handles the same sources cleanly.
**Master reference:** `cv/main_example.tex` (canonical CV with all competencies, experience, and achievements — use as source when building targeted CVs)

### Compile command
```bash
cd cv && lualatex -interaction=nonstopmode main_<company>.tex && cd ..
```

Expected output: `Output written on main_<company>.pdf (2 pages, ...)`. Any page count other than 2 is a failure that must be fixed before presenting to the user.

## Document Structure (moderncv banking)

```latex
\documentclass[11pt,a4paper,sans]{moderncv}
\moderncvstyle{banking}
\moderncvcolor{blue}

% Force first/last name AND section headings to render in blue on lualatex
\renewcommand*{\firstnamestyle}[1]{{\fontsize{34}{36}\bfseries\upshape\color{color1}#1}}
\renewcommand*{\lastnamestyle}[1]{{\fontsize{34}{36}\bfseries\upshape\color{color1}#1}}
\renewcommand*{\sectionstyle}[1]{{\sectionfont\color{color1}#1}}

\usepackage[utf8]{inputenc}
\usepackage{hyperref}
\hypersetup{
 colorlinks=true,
 linkcolor=blue,
 filecolor=magenta,
 urlcolor=blue,
 pdftitle={Valentine O. Owuor - CV},
 pdfpagemode=FullScreen,
}
\usepackage[scale=0.80]{geometry}
\usepackage{import}
\usepackage{needspace}

% Personal data
\name{Valentine}{O. Owuor}
\address{Nairobi, Kenya}{}{}
\phone[mobile]{+254 7XX XXX XXX}
\email{valentineowuor12@gmail.com}
\extrainfo{\href{https://linkedin.com/in/valentine-owuor}{LinkedIn}, \href{https://github.com/valentinus295}{GitHub}}

\begin{document}
\makecvtitle

% 1. Profile statement (1-3 lines, tailored per role)
% 2. Core competencies / skills (5-7 items, bold category labels)
% 3. Professional Experience (reverse chronological, 4-5 bullets for most recent, 2-3 for older)
% 4. Education (reverse chronological)
% 5. Languages
% 6. Selected Publications (2-3 most relevant)
% 7. References ("Available upon request.")

\end{document}
```

## Personal Data Reference
Use these fields exactly across all targeted CVs:
- **Name:** Valentine O. Owuor
- **Email:** valentineowuor12@gmail.com
- **Phone:** +254 7XX XXX XXX
- **LinkedIn:** https://linkedin.com/in/valentine-owuor
- **GitHub:** https://github.com/valentinus295
- **Address:** Nairobi, Kenya

## Spacing Guidelines

**Do not place `\vspace{...}` between `\item` entries inside an `itemize` list.** This occasionally produces an oversized gap before a single item; let moderncv use its native `\itemsep` instead.

Two patterns that are correct and should be kept:
- `\vspace{1pt}` immediately after `\section{...}` (between heading and first item)
- `\vspace{3pt}` between top-level `\cventry` blocks in Professional Experience or Education

## Section-by-Section Tailoring

### Profile Statement (most important customization)
3–4 lines right after `\makecvtitle`. Acts as an elevator pitch: why this candidate, for *this specific role*.

**For AI / Agent infrastructure roles:**
> Python engineer and AI systems builder with hands-on experience designing offline-first, voice-driven agent architectures. Built Hadhi as a multi-agent economic system (Ear → Linguist → Bookkeeper → Statistician → Advisor) on OpenClaw + Hermes, achieving a 71% accuracy pilot on a 500-trader dataset using a non-parametric credit-scoring method.

**For Voice AI / Conversational roles:**
> Voice AI engineer with production experience bridging Luo/Kiswahili ASR/TTS into a financial services workflow. Built real-time speech-to-report pipelines (Whisper + Coqui TTS) and evaluated accuracy on a 500-user informal-trader pilot. Comfortable from audio preprocessing through end-user deployment on Flutter.

**For Research / AI-for-science roles:**
> Research engineer with a NeurIPS 2025 AI4Science publication and first-author contributions in graph neural networks and evaluation harness design. Reduced metabolic pathway prediction error by 60% in a 12-week lab-integrated project. Seeking roles where rigorous experimentation meets production impact.

**For Developer tooling / platform roles:**
> Full-stack Python engineer who builds developer-facing tools end-to-end. Built a Django + Vue.js skill-assessment platform serving 400+ students, and open-sources agent frameworks through Cohusdex and Paperclip internals. Comfortable with REST APIs, Streamlit, and Python-first infrastructure.

### Core Competencies / Skills Section (5–7 items, bold category labels)
Reorder and emphasize based on the target role. Each item: bold label + specific tools/outcomes.

Example template:
```
\item \textbf{Agentic Systems \& orchestration}: Python, OpenClaw Hermes, Paperclip, multi-agent pipeline design (5-node architectures), RAG, Knowledge Graphs, LLM evaluation (lm-eval-harness)
\item \textbf{Voice AI \& ASR/TTS}: Whisper, Whisper.cpp (edge), Coqui TTS, multilingual audio pipelines, Flutter platform-channel integration
\item \textbf{ML \& Research}: PyTorch, PyTorch Geometric (GNNs), scikit-learn, graph neural networks, experimental design, statistical evaluation, non-parametric credit scoring (Sigma_1R)
\item \textbf{Full-stack Python \& Mobile}: FastAPI, Django, Flutter, SQLite, Streamlit, Gradio, REST/WebSocket APIs, git/GitHub Actions
\item \textbf{LaTeX \& Document Automation}: moderncv, document generation pipelines, PDF automation, structured technical writing
```

### Professional Experience (reverse chronological)
- **Most recent role:** 4–5 bullets
- **Previous roles:** 2–3 bullets
- **Older roles:** 1–2 bullets (1 line each)
- Emphasize measurable results: percentages, absolute counts, timeframes

**Relevance-weighted cutting rule:** Cut by signal, not by section order. For every candidate line:
1. Does it hit a named tool, keyword, or responsibility in the job ad? (Y/N)
2. Is this claim made anywhere else in the CV? (Y/N → duplicate cut)
3. Does the cover letter depend on this bullet? (Y/N → load-bearing)

Cut the lowest total-score line first, regardless of which section it sits in.

Order of cuts (easiest → last resort):
1. Redundancy (Core Competencies version of an experience bullet)
2. Profile-statement fluff (claims already covered by Publications or Skills)
3. Low-relevance experience bullets (does not touch posting keywords)
4. Low-relevance supporting content (unrelated certifications, languages that can be condensed)
5. Low-relevance publications (keep 1-2 that match posting)
6. Last-resort structural cuts (oldest education, tighten older role)

### Education
- Always include highest degrees
- For senior roles, keep brief (dates and titles only)
- Include thesis topics when relevant to the target role

### Languages
- **English** (native), **Kiswahili** (fluent), **Luo** (conversational — used in Hadhi ASR/TTS pipeline)

### Publications
- Select 2–3 most relevant publications (not always all)
- For non-academic roles, keep to 1–2 lines
- Include arXiv/workshop links where available

### Awards
- Keep format brief, one line each

### References
- List 1–2 references with name, title, organization, and contact
- End with: "More references are available upon request."

## Page Budget — Hard 2-Page Limit
The CV must fit exactly 2 pages. Use these content limits as a guide:

| Section | Max budget |
|---------|-----------|
| Profile statement | 3–4 lines |
| Skills | 5 items, each 1–2 lines |
| Most recent role | 4–5 bullets |
| Previous role | 2–3 bullets |
| Older roles | 1–2 bullets (1 line each) |
| Education | 2–3 entries |
| Publications | 2–3 entries |
| Awards | 3 entries, single line each |
| References | "Available upon request." (single line) |

**If in doubt, cut rather than squeeze.** Do not reduce geometry or remove `\vspace` to force-fit — it makes the CV look cramped.

## Compile-and-Inspect Loop (MANDATORY)
After writing the CV and before presenting to the user:
1. Run `lualatex -interaction=nonstopmode main_<company>.tex`
2. Check output page count: must be exactly 2
3. Read the PDF via the Read tool and visually inspect both pages
4. Check for orphaned entries: a `\cventry` title line must never sit alone at the bottom of page 1 with bullets on page 2

### Fixing Common Page-Break Problems

**Problem: entry title on page 1, bullets orphaned to page 2**
Add `\needspace{5\baselineskip}` immediately before the problematic `\cventry`:
```latex
\needspace{5\baselineskip}
\item{\cventry{2025--Present}{Founding Engineer}{Cohusdex}{Remote, Kenya}{}{...}}
```
Ensure `\usepackage{needspace}` is in the preamble.

**Problem: one trailing section spills to page 3 (e.g., References alone on page 3)**
Add `\enlargethispage{2\baselineskip}` before a late section (e.g., before `\section{Languages}`) to stretch page 2.

**Problem: 3 pages with significant content on page 3**
Cut content — do not compress geometry or `\vspace`. Use the relevance-weighted cutting rule above.

**Problem: content finishes early on page 2 (feels thin)**
Restore the highest-relevance item that was previously cut. A CV that ends mid-page 2 looks incomplete.

## Recommended Section Order

**For AI / agent infrastructure / technical roles:**
1. Profile statement / elevator pitch
2. Core competencies / Skills
3. Professional Experience (reverse chronological)
4. Education
5. Languages
6. Publications & Awards
7. References

**For research / academic-track roles:**
1. Profile statement
2. Core competencies / Skills
3. Education (credentials are a key qualifier)
4. Professional Experience
5. Publications & Awards
6. References
