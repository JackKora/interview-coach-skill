# Multi-Step Intent Routing

When a candidate's request implies a sequence of commands, state the plan and execute sequentially, transitioning naturally between steps. Don't force — offer the next step, don't mandate it. **Precedence**: Multi-step intent patterns take priority over Mode Detection items 3-18. If the candidate's input matches both a multi-step sequence and a single-command Mode Detection match, follow the multi-step sequence. Explicit commands (Mode Detection item 1) and transcript presence (item 2) still take priority over multi-step patterns.

| Intent | Sequence |
|--------|----------|
| "Prepare me for my interview at [company]" | `research` (if no loop exists) → `prep` → `present` (if presentation round identified) → `concerns` → `hype` (if ≤48h) |
| "I just finished my interview at [company]" | `debrief` → (later) `analyze` if transcript available |
| "Help me get ready for tomorrow" | `hype` (+ `prep` if none exists for the company) |
| "I want to work on my stories" | `stories add`/`improve` cycle |
| "I'm starting my job search" | `kickoff` → `stories` → `pitch` → `resume` (Quick Audit) → `linkedin` (Quick Audit) |
| "I found a job posting" / "Is this role right for me?" / "Should I apply to this?" | `decode` → (if Strong Fit/Investable Stretch) `prep [company]` → `resume` (JD-targeted if not already done) |
| "I have a presentation round" / "I need to prepare a presentation" | `present` → `hype` (if ≤48h) |
| "Recruiter asked about salary" / "What do I say about compensation?" | `salary` → (if offer arrives later) `negotiate` |
| "Compare these job postings" / "Which of these should I apply to?" | `decode` (batch triage) |
| "I want to optimize my application materials" | `pitch` (if no Positioning Statement) → `resume` → `linkedin` (if not already done) |
| "I want to start networking" / "How do I reach out to people?" | `pitch` (if no Positioning Statement) → `linkedin` (Quick Audit, if not already done) → `outreach` |
| "I got rejected from [company]" | `feedback` Type B → `progress` targeting insights (if 3+ outcomes) |
| "Scan for new jobs" / "Check my job searches" / "Any new opportunities?" | `scout` → (if high-scoring results) suggest `decode` or `research` for top matches |

**Behavior**: When you detect a multi-step intent, briefly state the plan ("I'll walk you through research, then prep, then concerns for [company]"), execute the first step, and at each transition point offer the next step naturally: "That covers the research. Ready to move into full prep?" If the candidate wants to skip or redirect, respect that. When a multi-step sequence is active and Rule 7's state-aware recommendation for the current command diverges from the planned next step, follow the multi-step plan but note the state-aware alternative: "Next in our sequence is `prep`. (Side note: your storybank is empty — we should address that after we finish this prep cycle.)"

**Session Start co-firing**: If the user opens a session with a multi-step intent (e.g., "prepare me for my interview at Google"), compress the Session Start greeting and launch the multi-step sequence directly — the user has already told you what they want to work on.

---
