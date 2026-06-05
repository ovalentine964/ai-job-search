# Cover Letter Templates and Tailoring Guide

## Template: Custom cover.cls (XeLaTeX)

Cover letters use a custom LaTeX document class (`cover.cls`) with Lato/Raleway fonts.

**Output file:** `cover_letters/cover_<company>_<role>.tex`
**Compile with:** XeLaTeX (cover.cls requires fontspec)
**Font directory:** `cover_letters/OpenFonts/fonts/`

### Compile command
```bash
cd cover_letters && xelatex -interaction=nonstopmode cover_<company>_<role>.tex && cd ..
```

Expected output: `Output written on cover_<company>_<role>.pdf (1 page, ...)`. Any page count other than 1 is a failure that must be fixed before presenting to the user.

## Compile-and-Inspect Loop (MANDATORY)

After writing the cover letter and before presenting to the user, always compile and visually inspect the PDF. Iterate until the layout is clean:
1. Run `xelatex -interaction=nonstopmode cover_<company>_<role>.tex`
2. Confirm page count is exactly 1 and compile succeeded
3. Read the PDF via the Read tool and visually check: signature fits at the bottom, no text cut off, bullet font matches body

### Known template pitfall: itemize inside `\lettercontent{}`

The `\lettercontent{}` macro appends `\\` to its argument. This breaks when the argument ends in `\end{itemize}` because there is no line to break after the environment closes.

**Wrong (breaks compile):**
```latex
\lettercontent{Here is how my experience maps:
\begin{itemize}
 \item ...
\end{itemize}}
```

**Correct — close \lettercontent{} before the list and wrap the list in Raleway-Medium font so typography stays consistent:**
```latex
\lettercontent{Here is how my experience maps:}

{\raggedright\fontspec[Path = OpenFonts/fonts/raleway/]{Raleway-Medium}\fontsize{11pt}{13pt}\selectfont
\begin{itemize}
 \item ...
\end{itemize}\par}
\vspace{6pt}

\lettercontent{[next paragraph]}
```

The font wrapper is mandatory. If you just move `\begin{itemize}` outside `\lettercontent{}` without the `\fontspec` block, bullets render in the default body font (Lato) and visually mismatch the rest of the letter.

## Document Structure (cover.cls)

```latex
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Cover Letter - [Company], [Role]
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

\documentclass[]{cover}
\usepackage{fancyhdr}

\pagestyle{fancy}
\fancyhf{}
\rfoot{Page \thepage \hspace{0pt}}
\thispagestyle{empty}
\renewcommand{\headrulewidth}{0pt}
\begin{document}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% TITLE NAME
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\namesection{}{\Huge{Valentine O. Owuor}}{ \href{mailto:valentineowuor12@gmail.com}{valentineowuor12@gmail.com} | +254 7XX XXX XXX | \urlstyle{same}\href{https://linkedin.com/in/valentine-owuor}{LinkedIn}
}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% MAIN COVER LETTER CONTENT
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

\currentdate{\today}
\lettercontent{Dear [Name/Hiring Manager],}

\lettercontent{[Opening paragraph. State the role and immediately connect your background to the role. Make it specific. 2–3 sentences max.]}

\lettercontent{[Body paragraph. Lead with the most relevant experience for this role. Use a bullet list for concrete achievements (3–5 bullets). Close the lettercontent before the bullet list and wrap it in the Raleway-Medium font wrapper.]}

{\raggedright\fontspec[Path = OpenFonts/fonts/raleway/]{Raleway-Medium}\fontsize{11pt}{13pt}\selectfont
\begin{itemize}
 \item \textbf{Achievement 1}: [Title with measurable outcome: e.g. "Delivered a 60% accuracy gain in pathway prediction by building a graph neural network model (PyTorch, PyTorch Geometric) adopted as the lab's standard tool."]
 \item \textbf{Achievement 2}: [Another concrete example]
 \item \textbf{Achievement 3}: [A third example]
\end{itemize}\par}
\vspace{6pt}

\lettercontent{[Connection to company. Why this company specifically? Reference their mission, product, or market. 2–3 sentences. Forward-looking: what will you do for them?]}

\lettercontent{[Personal fit. Behavioral strengths — e.g. self-directed builder, collaborative leader, fast learner. Connect to the role's likely team culture. 2–3 sentences.]}

\lettercontent{I look forward to hearing from you.}

\begin{flushright}
\closing{Kind regards,\\\}
\signature{Valentine O. Owuor}
\end{flushright}
\end{document}
```

## Key Commands Reference

| Command | Purpose |
|---------|---------|
| `\namesection{}{Name}{contact info}` | Header with name and contact |
| `\currentdate{date}` | Date field (use `\today` or explicit date) |
| `\lettercontent{text}` | Body paragraph (adds spacing after) |
| `\closing{text}` | Closing line |
| `\signature{name}` | Printed name below signature |

## Salutation
- If you know the hiring manager's name: "Dear [First Last],"
- If you know the team: "Dear [Company] hiring team,"
- Generic: "Dear [Company]," (avoid "To whom it may concern")

## Length — Hard 1-Page Limit
- **Target: 1 page including signature block**
- **Word budget: 250–300 words** of body text (not counting LaTeX markup). 350 words will overflow.
- Always count: opening paragraph + bullet list paragraph + closing paragraph = 3 blocks. Add a 4th only if the others are short.
- When adding company-specific content, trim other content to compensate

## Line Spacing
- Add `\usepackage{setspace}` and `\setstretch{1.0}` if the letter is long and needs to fit
- Use `\vspace{.5cm}` between major sections for readability (only if space permits)

## Bullet Lists
- Place `\begin{itemize}...\end{itemize}` **outside** a `\lettercontent{}` block, wrapped in the Raleway-Medium `\fontspec` block (see template and known pitfall above)
- 3–5 bullets is ideal
- Start each bullet with bold label or action verb
- Use `\textbf{Label:}` for category-style bullets

## LaTeX Special Characters
- Underscore: `\_`
- Ampersand: `\&`

## Checklist Before Finalizing
- [ ] No em-dashes (use commas or periods instead)
- [ ] No cliches or empty filler
- [ ] Every claim backed by specific example (preferably with a metric)
- [ ] Forward-looking framing: focuses on tasks you will solve for them
- [ ] Motivation section references this specific company's mission/values
- [ ] Company name and role are correct throughout
- [ ] Date is current
- [ ] Fits on one page
- [ ] Language matches the job posting language
- [ ] Salutation is appropriate (named person if possible)
- [ ] Agentic coding references mention **OpenClaw**, **Paperclip**, and **Hermes** by name

## Submission Guidelines (Best Practice)
- Submit only the documents the employer requests
- Export as PDF to preserve formatting
- Name files clearly: "Valentine Owuor — CV" and "Valentine Owuor — Cover Letter"
- Follow all employer instructions regarding anonymity or specific materials
