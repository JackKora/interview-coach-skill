Load this file when `kickoff` creates state, when a command must create a missing state file or section, or when an exact field/table format is needed. These are instructions describing generated user data; this file stays under `references/` and must never be copied into `coaching_state/`.

# Coaching State Schemas

These are creation templates, not a demand to rewrite older state. Except for the root routing keys in `index.md`, missing fields and sections mean unknown or not-yet-created. Preserve sparse records, legacy aliases, extra columns, and unknown sections. Bring only the record already being updated to the current format.

#### coaching_state/index.md

```markdown
# Coaching State — [Name]
Schema version: 1
Last updated: [date]
Status: [Active / Archived / Unknown]

## Quick Context
- Cycle status: [active_current_search / imported_previous_search_reconciliation_required]
- Last session: [date], commands: [list]
- Drill stage: [N]
- Real interviews logged: [N]
- Current bottleneck: [dimension]
- Sessions since last meta-check: [N]
- Pending outcomes: [company list or "none"]
- Next interview: [company, date, or "none scheduled"]
- Interview timeline: [date, "ongoing", or "unknown"]

## Files
| File | Contains |
|------|----------|
| profile.md | Profile, Resume Analysis, Active Coaching Strategy, Calibration State, Drill Progression |
| storybank.md | Storybank index + Story Details |
| interviews.md | Interview Loops, Outcome Log |
| intelligence.md | Interview Intelligence |
| scores.md | Score History |
| tracking.md | Session Log, Meta-Check Log, Coaching Notes |
| opportunities.md | Scout Config, Scout Opportunities |
| opportunities_bad_fit.md | Below-threshold scout opportunities (dedup index) |
| jd_analyses.md | JD Analysis sections |
| assets.md | LinkedIn, Resume, Positioning, Outreach, Comp, Presentation |
| archive.md | Append-only verbatim archive batches (when archival has occurred) |
```

#### coaching_state/profile.md

```markdown
## Profile
- Target role(s):
- Seniority band:
- Track: Quick Prep / Full System
- Feedback directness: [1-5]
- Interview timeline: [date or "ongoing"]
- Time-aware coaching mode: [triage / focused / full]
- Interview history: [first-time / active but not advancing / experienced but rusty]
- Biggest concern:
- Known interview formats: [e.g., "behavioral screen, system design (verbal walkthrough)" — updated by Format Discovery Protocol during prep/mock]
- Anxiety profile: [confident-underprepared / anxious-specific / generalized / post-rejection / impostor — set by hype, reused in subsequent sessions]
- Career transition: [none / function change / domain shift / IC↔management / industry pivot / career restart — set by kickoff]
- Transition narrative status: [not started / in progress / solid — set by kickoff, updated by pitch/stories]

## Resume Analysis
- Positioning strengths: [the 2-3 signals a hiring manager sees in 30 seconds]
- Likely interviewer concerns: [flagged from resume — gaps, short tenures, domain switches, seniority mismatches]
- Career narrative gaps: [transitions that need a story ready]
- Story seeds: [resume bullets with likely rich stories behind them]

## Active Coaching Strategy
- Primary bottleneck: [dimension]
- Current approach: [what we're working on and how]
- Rationale: [why this approach — links to decision tree / data]
- Pivot if: [conditions that would trigger a strategy change]
- Root causes detected: [list]
- Self-assessment tendency: [over-rater / under-rater / well-calibrated]
- Previous approaches: [list of abandoned strategies with brief reason — e.g., "Structure drills — ceiling at 3.5, diminishing returns"]

## Calibration State

### Calibration Status
- Current calibration: [uncalibrated / calibrating / calibrated / miscalibrated]
- Last calibration check: [date]
- Data points available: [N] real interviews with outcomes

### Scoring Drift Log
| Date | Dimension | Direction | Evidence | Adjustment |

### Calibration Adjustments
| Date | Trigger | What Changed | Rationale |

### Cross-Dimension Root Causes (active)
| Root Cause | Affected Dimensions | First Detected | Status | Treatment |

### Unmeasured Factor Investigations
| Date | Trigger | Hypothesis | Investigation | Finding | Action |

## Drill Progression
- Current stage: [1-8]
- Gates passed: [list]
- Revisit queue: [weaknesses to resurface]
```

#### coaching_state/storybank.md

```markdown
## Storybank
| ID | Title | Primary Skill | Secondary Skill | Earned Secret | Strength | Use Count | Last Used |
|----|-------|---------------|-----------------|---------------|----------|-----------|-----------|
[rows — compact index. Use Count tracks total times used in real interviews (incremented via debrief). Full column spec in references/storybank-guide.md — the guide adds Impact, Domain, Risk/Stakes, and Notes. Add extra columns as stories are enriched.]

### Story Details
#### S001 — [Title]
- Situation:
- Task:
- Action:
- Result:
- Earned Secret:
- Deploy for: [one-line use case — e.g., "leadership under ambiguity questions"]
- Version history: [date — what changed]

[repeat for each story]
```

#### coaching_state/scores.md

```markdown
## Score History
### Historical Summary (optional derived navigation)
[Narrated trend summary of active and archived sessions — direction per dimension, inflection points, what caused shifts. This never replaces raw rows; cite archive batch IDs when used.]

### Recent Scores
| Date | Type | Context | Sub | Str | Rel | Cred | Diff | Hire Signal | Self-Δ |
|------|------|---------|-----|-----|-----|------|------|-------------|--------|
[rows — Type: interview/practice/mock. Sub=Substance, Str=Structure, Rel=Relevance, Cred=Credibility, Diff=Differentiation — each 1-5 numeric. Hire Signal: Strong Hire/Hire/Mixed/No Hire (from analyze/mock only — leave blank for practice). Self-Δ: over/under/accurate (>0.5 delta from coach scores = over or under; within 0.5 = accurate). Keep a useful active window; older raw rows may move verbatim to archive.md.]
```

#### coaching_state/interviews.md

```markdown
## Interview Loops (active)
### [Company Name] — [Role]
- Loop ID: [stable unique ID, e.g. company-role-cycle slug]
- Role: [role title]
- Status: [Decoded / Researched / Applied / Interviewing / Offer / Closed]
- Rounds completed: [list with dates]
- Round formats:
  - Round 1: [format, duration, interviewer type — e.g., "Behavioral screen, 45min, recruiter"]
  - Round 2: [format, duration, interviewer type]
- Stories used: [S### per round]
- Concerns surfaced: [ranked list from `concerns` — severity + counter strategy, or from analyze/rejection feedback]
- Interviewer intel: [LinkedIn URLs + key insights, linked to rounds]
- Prepared questions by round: [round ID/type → top 3 from `questions` if run]
- Next round: [date, format if known]
- Fit verdict: [from research or prep — Strong / Investable Stretch / Long-Shot Stretch / Weak]
- Fit confidence: [Limited — no JD / Medium — JD + resume / High — JD + resume + storybank]
- Fit signals: [1-2 lines on what drove the verdict]
- Structural gaps: [gaps that can't be bridged with narrative, if any]
- Date researched: [date, if `research` was run]

## Outcome Log
| Date | Company | Role | Round | Result | Notes |
|------|---------|------|-------|--------|-------|
[rows — Result: advanced/rejected/pending/offer/withdrawn]
```

#### coaching_state/intelligence.md

```markdown
## Interview Intelligence

### Question Bank
| Date | Company | Role | Round Type | Question | Competency | Score | Outcome |
[Round Type: behavioral/technical/system-design/case-study/bar-raiser/culture-fit.
 Score: average across 5 dims (e.g., 3.4), or "recall-only" for debrief-captured questions.
 Outcome: advanced/rejected/pending/unknown — updated when known.]

### Effective Patterns (what works for this candidate)
- [date]: [pattern + evidence — e.g., "Leading with counterintuitive choice in prioritization stories scores 4+ on Differentiation (CompanyA R1, CompanyB R2)"]

### Ineffective Patterns (what keeps not working)
- [date]: [pattern + evidence — e.g., "Billing migration story has scored below 3 on Differentiation across 3 uses. Retire or rework."]

### Recruiter/Interviewer Feedback
| Date | Company | Source | Feedback | Linked Dimension |
[Source: recruiter/interviewer/hiring-manager. Keep verbatim when possible.]

### Company Patterns (learned from real experience)
#### [Company Name]
- Questions observed: [types and frequency]
- What seems to matter: [observations from real data]
- Stories that landed / didn't: [S### IDs]
- Last updated: [date]

### Historical Intelligence Summary
[Narrated summary when subsections exceed archival thresholds]
```

#### coaching_state/tracking.md

```markdown
## Session Log
### Historical Summary (optional derived navigation)
[Brief narrative of earlier sessions. This never replaces raw session rows; cite archive batch IDs when used.]

### Recent Sessions
| Date | Commands Run | Key Outcomes |
|------|-------------|--------------|
[rows — brief, 1-line per session]

## Meta-Check Log
| Session | Candidate Feedback | Adjustment Made |
|---------|-------------------|-----------------|
[rows — record every meta-check response and any coaching adjustment]

## Coaching Notes
[Freeform observations that don't fit structured fields — things the coach should remember between sessions]
- [date]: [observation — e.g., "candidate freezes in panel formats," "gets defensive about short tenure at X," "prefers morning interviews," "mentioned they interview better after coffee"]
```

#### coaching_state/opportunities.md

```markdown
## Scout Config
- Search URLs:
  - LinkedIn: [url]
  - [other sources]: [urls]
- Fit threshold: [1-5]
- Last scan date: [date]

## Scout Opportunities
| Date | Company | Title | Score | Rationale | URL | Status |
|------|---------|-------|-------|-----------|-----|--------|
[rows — Status: New / Reviewed / Pursuing / Passed / Archived. New discoveries enter here when above threshold. A complete tracked row may remain canonical here after a later threshold increase; the current threshold controls reporting, not destructive movement. Initially below-threshold discoveries are stored in opportunities_bad_fit.md for dedup.]
```

#### coaching_state/opportunities_bad_fit.md

```markdown
# Below-Threshold Opportunities
Last updated: [date]

| Date | Company | Title | Score | Rationale |
|------|---------|-------|-------|-----------|
[rows — dedup index for below-threshold scout results. No archival — grows unbounded by design.]
```

#### coaching_state/jd_analyses.md

```markdown
## JD Analysis: [Company] — [Role]
- Date: [date]
- Depth: [Quick Scan / Standard / Deep Decode]
- Fit verdict: [Strong Fit / Investable Stretch / Long-Shot Stretch / Weak Fit]
- Top competencies: [top 3 in priority order]
- Frameable gaps: [list]
- Structural gaps: [list]
- Unverified assumptions: [count of LOW/UNKNOWN items]
- Batch triage rank: [rank/total, if applicable]

[Multiple JD Analysis sections can exist — one per company+role]

### Past JD Analyses (optional navigation index)
| Date | Company | Role | Fit Verdict | Archive Batch |
[rows — links to complete verbatim analyses in archive.md; never the only surviving copy]
```

#### coaching_state/archive.md

```markdown
# Coaching State Archive

Append-only. Existing archive batches are immutable.

## Archive Batch: [unique ID]
- Archived: [date/time]
- Source file: [coaching_state/file.md]
- Source section: [exact heading or table name]
- Reason: [closed/inactive/threshold navigation]
- Record count: [N]

<!-- BEGIN VERBATIM ARCHIVE -->
[exact source table header + separator + selected row text, or exact complete heading + body]
<!-- END VERBATIM ARCHIVE -->

[repeat; never edit or delete an earlier batch]

## Archive Amendment: [unique ID]
- Amended: [date/time]
- Original record: [archive batch ID or immutable cycle-id/path]
- Record identity: [stable ID or company + role + round + date]
- Reason: [new outcome / correction / added evidence]

<!-- BEGIN APPEND-ONLY AMENDMENT -->
[new fact or correction; never rewrite the original batch]
<!-- END APPEND-ONLY AMENDMENT -->
```

#### coaching_state/archive/cycles/[cycle-id]/

When `kickoff` starts a genuinely new search over existing state, preserve the previous cycle here before initializing the new active files. Copy every top-level state file byte-for-byte, including `archive.md` when present, and add `manifest.sha256` containing the source path, byte count, and SHA-256 hash. Verify the archived copies before changing active state. Cycle archives are immutable and ignored by normal command routing; `reflect`, historical questions, and explicit cross-cycle comparisons may read them.

#### coaching_state/assets.md

```markdown
## LinkedIn Analysis
- Date: [date]
- Depth: [Quick Audit / Standard / Deep Optimization]
- Overall: [Strong / Needs Work / Weak]
- Recruiter discoverability: [Strong / Moderate / Weak]
- Credibility on visit: [Strong / Moderate / Weak]
- Differentiation: [Strong / Moderate / Weak]
- Top fixes pending: [1-3 line items]
- Positioning gaps: [resume ↔ LinkedIn inconsistencies, if assessed]

## Resume Optimization
- Date: [date]
- Depth: [Quick Audit / Standard / Deep Optimization]
- Overall: [Strong / Needs Work / Weak]
- ATS compatibility: [ATS-Ready / ATS-Risky / ATS-Broken]
- Recruiter scan: [Strong / Moderate / Weak]
- Bullet quality: [Strong / Moderate / Weak]
- Seniority calibration: [Aligned / Mismatched]
- Keyword coverage: [Strong / Moderate / Weak]
- Top fixes pending: [1-3 line items]
- JD-targeted: [yes — which JD / no]
- Cross-surface gaps: [resume ↔ LinkedIn inconsistencies, if assessed]

## Positioning Statement
- Date: [date]
- Depth: [Quick Draft / Standard / Deep Positioning]
- Core statement: [the full hook + context + bridge — 30-45 second version]
- Hook (10s): [the curiosity-gap opener alone]
- Key differentiator: [one sentence]
- Earned secret anchor: [the earned secret or spiky POV powering the positioning]
- Target audience: [primary audience this was optimized for]
- Variant status: [which variants were produced]
- Consistency status: [aligned / gaps identified — brief summary]

## Outreach Strategy
- Date: [date]
- Depth: [Quick / Standard / Deep]
- Positioning source: [Positioning Statement / Resume Analysis fallback]
- Message types coached: [list]
- Targets contacted: [people/companies]
- Channel strategy: [primary channels]
- Follow-up status: [pending follow-ups with timing]
- LinkedIn profile flagged: [yes/no]
- Key hooks identified: [1-2 reusable positioning hooks]

## Comp Strategy
- Date: [date]
- Depth: [Quick Script / Standard / Deep Strategy]
- Target range: [bottom / target / stretch — or "not yet researched"]
- Range basis: [sources used]
- Research completeness: [none / partial / thorough]
- Stage coached: [application / recruiter screen / mid-process / general]
- Jurisdiction notes: [relevant info, if applicable]
- Scripts provided: [which stages covered]
- Key principle: [the most important takeaway]

## Presentation Prep: [Topic / Company — Role — Round]
- Loop ID: [stable loop ID, or "none" for general presentation coaching]
- Role: [role title, or "none"]
- Round ID/type: [round identity, or "none"]
- Date: [date]
- Depth: [Quick Structure / Standard / Deep Prep]
- Framework: [selected narrative arc]
- Time target: [X min presentation + Y min Q&A]
- Content status: [outline only / full content / talk track reviewed]
- Top predicted questions: [top 3]
- Key adjustment: [single biggest change recommended]
```
