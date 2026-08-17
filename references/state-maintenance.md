# State Maintenance and Archival

Maintenance improves active-file navigation; it never authorizes destroying history. Thresholds are review triggers, not deletion rules. A summary is derived context and must never replace the only raw copy of a row, pattern, note, analysis, or presentation record.

## Append-Only Archive

Use `coaching_state/archive.md` for inactive raw records. It is user state and follows the archive schema in `references/state-schemas.md`. Never edit or delete an existing archive batch. Normal command reads use active files; `progress`, `reflect`, audits, and historical questions may read the archive when needed.

For every archival batch:

1. Read both the source file and `archive.md` if it exists.
2. Select complete records only. For tables, archive row text verbatim and include the source table header and separator in the batch. For prose or repeated sections, copy the complete heading and body verbatim.
3. Append the new batch to `archive.md` first, with a unique archive ID, source file, source section, date, and reason.
4. Re-read the archive and verify the copied raw text exactly matches the source selection. Verify row/record counts and the full-line multiset; duplicates in the source must remain duplicates in the archive.
5. Only after successful verification, remove the exact archived records from the active section. Retain its heading and table header. Verify that active plus archived counts equal the pre-archive count.
6. Optionally add or refresh a clearly labeled summary in the active file, but never present it as the raw record.
7. If any verification fails, leave the source unchanged. Never partially archive a record.

Archive only closed, inactive, or old records. Never archive pending outcomes, active interview loops, upcoming presentation prep, unresolved feedback, or records needed by the current coaching strategy. Archival must preserve identifiers and company/role names so records remain retrievable.

If new evidence later changes an archived record, never edit its immutable batch or cycle copy. Append an `Archive Amendment` using the schema in `references/state-schemas.md`, keyed to the original batch or cycle path and record identity, and record the new canonical fact in the appropriate active log when applicable. Every archived read must also retrieve amendments matching that original record and apply them in timestamp order; the latest amendment is authoritative while the original history remains intact.

## Review Thresholds

- `scores.md`: when active Score History exceeds 15 rows, move the oldest complete rows to the append-only archive while retaining at least 10 recent rows.
- `tracking.md`: when active Session Log exceeds 15 rows, archive the oldest complete rows while retaining at least 10 recent rows.
- `intelligence.md`:
  - Question Bank over 30 rows: archive complete rows older than 3 months while retaining at least 20 recent rows.
  - Effective or Ineffective Patterns over 10 entries: archive only superseded or inactive entries verbatim. Keep current patterns; an optional synthesis may link to archive batch IDs.
  - Recruiter/Interviewer Feedback over 15 rows: archive old closed-loop rows while retaining at least 10 recent rows.
  - Closed-loop Company Patterns may be moved as complete verbatim sections; never compress them in place.
- `jd_analyses.md`: when active JD analyses exceed 10, move complete analyses for roles not pursued or with Closed/Archived loops to the archive. Never reduce them to only company, role, verdict, and date.
- `assets.md`: completed Presentation Prep may be archived only as a complete verbatim section after the corresponding round is closed. Upcoming or active presentation material stays active.

`opportunities_bad_fit.md` remains an unbounded dedup index unless a future workflow defines a lossless archive-aware dedup lookup.

Load this file during `progress`, or when a state file already being read crosses a threshold. Maintenance is optional for completing `progress`: if lossless archival cannot be verified, skip maintenance and continue the coaching workflow with state unchanged. Do not perform speculative size scans at every session start.
