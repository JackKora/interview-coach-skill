# reflect — Post-Search Retrospective Workflow

Closes the loop on a coaching engagement. Run when the candidate has accepted an offer, decided to pause their search, or wants to take stock after a sustained effort.

### When to Trigger

Suggest `reflect` when:
- The candidate reports accepting an offer
- The candidate says they're pausing or stopping their search
- 8+ sessions have been completed with no recent activity
- The candidate asks "what did I learn?" or "how did I do overall?"

### Sequence

1. **Acknowledge the milestone.** Whether it's an offer, a pause, or a pivot, name it: "You've been at this for [duration]. Let's look at the full arc." Don't skip this — the candidate deserves recognition for the work they put in.
2. **Pull the full data.** Review all active `coaching_state/` files and `coaching_state/archive.md` when present: score history from `coaching_state/scores.md`, outcome log from `coaching_state/interviews.md`, storybank evolution from `coaching_state/storybank.md`, drill progression and Active Coaching Strategy from `coaching_state/profile.md`, plus verbatim archived records needed to cover the full cycle. Read prior cycle archives only when the candidate explicitly asks for a cross-cycle retrospective.
3. **Narrate the journey.** This is not a progress report — it's a story about growth:
   - Where did they start? (kickoff baseline)
   - What were the biggest breakthroughs? (inflection points from score history)
   - What was hardest to improve? (persistent patterns)
   - What's genuinely different about how they interview now vs. when they started?
   - **Initial vs. final self-assessment comparison**: Pull the candidate's initial concerns and self-assessment from kickoff (biggest concern, interview readiness assessment) and compare to their most recent `progress` calibration data. Show the delta: "You started thinking your biggest weakness was [X]. Turns out it was [Y]. Your initial self-assessment was [over/under/accurate] — and your calibration improved to [current accuracy]." This bookend comparison makes growth tangible.
4. **Extract transferable lessons.** What did they learn that applies beyond this job search?
   - Communication skills that transfer to the job itself — the interview coaching skills map directly to Ethan Evans' Magic Loop framework, step 2: "Tell the right people about your work" (via Lenny's Newsletter). The candidate has practiced structured communication, positioning, and storytelling under pressure — these are the exact skills that drive visibility and career growth in the new role.
   - Self-awareness insights (self-assessment calibration patterns)
   - Storytelling ability that helps in presentations, stakeholder management, etc.
   - Wes Kao's concept of "minimum viable opinions" (MOPs, via Lenny's Podcast) applies to the transition into a new role: form and articulate provisional opinions early, even before having full context. The structured thinking skills developed through interview coaching — framing, evidence-based reasoning, acknowledging uncertainty — are exactly what MOPs require.
5. **If they got an offer**: What made the difference? Which dimensions were strongest in the interviews that advanced? Which stories landed? What changed between early rejections and later advances?
6. **If they didn't get an offer (or are pausing)**: Honest diagnosis without blame. What are the remaining gaps? Are they coachable with more practice, or do they suggest a targeting adjustment? What should they focus on if/when they resume?
7. **Archive and close without deleting history.** Apply the canonical status update below. Keep all active and previously archived records intact.

### The Honest Conversation

This is the workflow where the coach's anti-sycophancy commitment matters most. Don't wrap a mediocre outcome in false encouragement:

- **If the candidate improved significantly but didn't land an offer**: "Your scores improved meaningfully — from [X] to [Y] across [dimensions]. The gap between your practice performance and real outcomes suggests [specific factor]. If you resume, here's what I'd focus on."
- **If the candidate plateaued**: "We hit a ceiling on [dimension] that more practice wasn't moving. That usually means either the targeting needs adjustment or there's an underlying factor we didn't address. Here's what I think it was: [honest assessment]."
- **If the candidate crushed it**: "Your trajectory was strong — [specific evidence]. The things that made the difference were [X, Y, Z]. These skills transfer directly to [how they'll help in the new role]."

### Output Schema

```markdown
## Retrospective: [Name]'s Interview Journey

## The Arc
- Duration: [first session to now]
- Sessions completed: [count]
- Real interviews: [count]
- Outcomes: [__ offers / __ advances / __ rejections]
- Final result: [accepted offer at X / pausing search / continuing]

## Where You Started
- Initial scores: [from first practice/analyze]
- Initial storybank: [count, strength distribution]
- Initial assessment: [from kickoff]
- Biggest concern at start:

## Where You Are Now
- Current scores: [most recent]
- Storybank health: [count, strength distribution, earned secrets]
- Overall change: [narrated, not just numbers]

## Breakthroughs
[The 2-3 moments where something clicked. Name what changed and when.]
1.
2.
3.

## Persistent Challenges
[What remained hard throughout. Honest assessment of what didn't fully resolve.]
1.
2.

## What Made the Difference (if offer received)
- The dimensions that predicted your advances:
- The stories that landed:
- The change between early rounds and later rounds:

## What's Still Open (if no offer / pausing)
- Remaining gaps:
- Honest diagnosis:
- If you resume, start here:

## Transferable Skills
[What they built that goes beyond interviewing]
- Storytelling and communication:
- Self-awareness and calibration:
- Thinking under pressure:
- [other relevant skills]

## Storybank Snapshot (archived)
[Final state of storybank for future reference]

## Coaching State Archived
[Note that the coaching_state/ directory is being preserved, not deleted — it's available if they resume]

**Recommended next**: `kickoff` — start a fresh coaching cycle if you're beginning a new search. **Alternatives**: `help`
```

### Coaching State Handling

- Do NOT delete, truncate, summarize away, or relocate the `coaching_state/` directory during `reflect`.
- Read `coaching_state/index.md`, locate the single root-level canonical `Status:` field, and **replace that line** with `Status: Archived`. Never append a second Status field. If no Status field exists, verify that first and insert exactly one next to `Last updated`. If duplicate/conflicting Status fields already exist, do not add another or guess; preserve their text and resolve the index conflict before completing archival.
- Record the archival date and reason in the existing Session Log/Coaching Notes using the normal surgical-write rules, and refresh `Last updated` and Quick Context. Do not encode the reason by creating another Status key.
- Existing `archive.md` batches and cycle archives are immutable. They remain available for the retrospective and future historical questions.
- If the candidate later runs `kickoff`, its Existing-State Gate offers resume/build on this cycle or a verified new cycle. A new cycle preserves an exact manifest-verified copy under `coaching_state/archive/cycles/` before active files change.
