# Job Scraper

**name:** job-scraper
**description:** Scrapes the web for 2026 internship positions matching Valentine O. Owuor's profile across Kenya and East Africa. Deduplicates across runs. Triggers on: job scrape, find jobs, search jobs, new jobs, job search, scrape jobs, /scrape
**allowed-tools:** Read, Write, Edit, Glob, Grep, WebFetch, WebSearch, Agent, AskUserQuestion

---

## Mission
Find 2026 internships in AI, ML, voice AI, agentic systems, and software engineering that are compatible with a final-year BSc CS student graduating December 2026, Kenya-based, open to fully remote roles. Filter aggressively: this repo only wants internships.

## Invocation

The user triggers this skill by saying things like:
- "Find new jobs"
- "Any new internships?"
- "/scrape"
- "Scrape the boards"

Optional arguments:
- A focus area, e.g. "/scrape voice AI" or "/scrape Flutter"
- "broad" to run all search categories
- "kenya" to focus only on Kenya roles
- "remote" to focus only on fully remote roles

---

## Execution Steps

### Step 0: Load State

1. Read `job_scraper/seen_jobs.json` (create if missing — see structure below)
2. Read `job_search_tracker.csv` to extract already-applied companies+roles
3. Read `search-queries.md` (this directory) for the search strategy

### Eligibility Filter (Apply Before Fetching - CRITICAL)

Run this filter BEFORE adding a result to seen_jobs.json. Only evaluate fit for results that pass eligibility.

**PASS ONLY IF ALL conditions are met:**
- **PAID**: the posting explicitly states stipend, salary, allowance, honorarium, or "paid internship". REJECT if labelled "unpaid", "voluntary", "no stipend", or has zero compensation mentioned. Paid-only is non-negotiable.
- **DOMAIN ALIGNED**: the role is in AI/ML, voice AI, agentic systems, data science, research engineering, software engineering (Python/Flutter/full-stack), or developer tooling. REJECT if the role is outside tech (e.g. marketing, sales, HR, general business).
- Role type: intern, internship, graduate trainee, fellowship, placement, student program
- Location: Kenya, Remote, OR hybrid with ≤2 in-person days/week
- Deadline is in the future or cannot be determined
- Posted within the last 14 days (or date unknown but deadline open)
- Does NOT require 3+ years of production experience
- Accepts final-year students (mention of Class of 2026, graduating Dec 2026, or no degree-completion requirement)

**REJECT (do not add to seen_jobs, skip entirely):**
- Full-time permanent role without an explicit internship track
- **Unpaid / voluntary / no stipend mentioned** (paid-only: this is non-negotiable)
- **Domain mismatch**: role is outside AI/ML/voice/agentic/data science/software engineering (e.g. marketing, sales, HR, general business)
- Requires completed degree (not compatible with "graduating Dec 2026")
- Deadline has passed
- Requires relocation outside Kenya/East Africa AND is not fully remote
- Requires 3+ years of production experience or senior-level tooling

### Step 1: Search

Run **WebSearch** queries from `search-queries.md`. By default, run the top 4 priority categories (Kenya internship boards + LinkedIn). If the user said "broad", run all categories.

For each search:
- Use WebSearch with site-specific and keyword-specific queries
- Target Kenya / East Africa first, then remote globally
- Look for postings that are internships
- Look for postings from the last 14 days
- Note the application deadline where visible

### Step 2: Fetch & Parse

For each promising result from Step 1:
- Use WebFetch to retrieve the job posting page
- Extract: **job title**, **company**, **location**, **posting date** (or "recent"), **URL**, **key requirements** (brief), **application deadline** (if listed), **role type label** (intern/graduate/etc.)
- Apply the Eligibility Filter above. If REJECTED, log as "rejected" in seen_jobs.json with reason, do NOT present to user.
- If PASS, proceed to deduplication check
- Skip if the URL or company+title combo already exists in `seen_jobs.json` "seen" list
- Skip if the company+role already appears in `job_search_tracker.csv`

### Step 3: Quick Fit Assessment

For each new eligible job, do a rapid fit check (NOT the full evaluation from `04-job-evaluation.md` — just a quick signal):

| Signal | Meaning |
|--------|---------|
| **High match** | Role directly involves your core skills (Python, AI/ML, voice, agentic, Flutter, FastAPI, research) and is explicitly labelled as intern/fellowship |
| **Medium match** | Role is adjacent (other software engineering, data science, analytics) and explicitly an internship |
| **Low match** | Role requires significant skills you lack, or is a borderline call on role type |

### Step 4: Deduplicate & Store

1. Add ALL fetched jobs (eligible and rejected) to `seen_jobs.json`:
```
{
 "seen": {
 "<url_hash_or_company_title_key>": {
     "title": "...",
     "company": "...",
     "country": "Kenya",
     "url": "...",
     "deadline": "YYYY-MM-DD or null",
     "first_seen": "YYYY-MM-DD",
     "role_type": "intern|fellowship|placement|graduate_trainee",
     "eligibility_status": "pending|pass|reject",
     "reject_reason": "... or null",
     "fit": "high/medium/low",
     "status": "new|skipped|evaluated",
     "notes": "..."
   }
 }
}
```

2. Only present jobs with `eligibility_status: "pass"` AND `status: "new"` to the user.

### Step 5: Present Results

Present new jobs in a table sorted by fit (high first):

```markdown
## New Internship Matches - YYYY-MM-DD

Found X new positions (Y high, Z medium, W low match | R rejected as non-intern).

| # | Fit | Role | Company | Country | Type | Deadline | URL |
|---|-----|------|---------|---------|------|----------|-----|
| 1 | High | ... | ... | Kenya | intern | 2026-07-15 | [Link](...) |

### High-Match Highlights
For each high-match job, add 2-3 bullets:
- Why it matches your profile
- Key requirements to check
- Any flags to address

### Medium-Match Opportunities
[Brief list]

### Skipped (Non-Internship) — FYI
X postings were filtered out because they are full-time/contract roles, not internships.
```

After presenting, ask:
> "Want me to evaluate any of these in detail? Just give me the number(s)."

If the user picks a number (or references), invoke the **job-application-assistant** skill workflow (fit evaluation first, then CV + cover letter if approved).

### Step 6: Update Tracker (Optional)

If the user decides to apply to any job, add a row to `job_search_tracker.csv`.

---

## Important Rules

1. **Never fabricate job postings.** Only present jobs found via actual WebSearch/WebFetch results.
2. **Respect deduplication.** Always check seen_jobs.json AND job_search_tracker.csv before presenting.
3. **Eligibility filter is mandatory and runs FIRST.** Never present a non-internship role to the user.
4. **Deadline filter.** If a posting's deadline has passed, mark rejected in seen_jobs.json with reason "expired deadline".
5. **Be efficient with WebFetch.** Don't fetch every search result. Use titles and snippets to pre-filter before fetching.
6. **Parallel searches.** Use the Agent tool or parallel WebSearch calls to speed up the search phase.
7. **Log rejections.** Even non-intern roles should be recorded in seen_jobs.json as "reject" with a reason. This builds a richer signal over time.
8. **No relocation-only roles.** If a role requires physical relocation outside Kenya and is not remote, reject with reason "requires relocation".
