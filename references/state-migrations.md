# State Migrations

Current state schema version: **1**.

Load this file only when state exists but `coaching_state/index.md` is missing, when legacy `coaching_state.md` exists, when the index has no `Schema version`, or when its version is older than the current version. Schema versions describe storage compatibility, not whether every optional field in the current creation templates is present.

## Safety Contract

- A split `coaching_state/` directory is compatible with version 1 when its Markdown is readable and its root index can route to the preserved state. Sparse records, older headings, missing optional fields, extra fields, and unknown sections are valid state—not reasons to rewrite history.
- Missing optional data means **unknown**. Add a current optional field only when creating a record or naturally updating that record; never bulk-fill historical records with guessed defaults.
- Preserve unknown content and existing values. Make the smallest compatible change.
- Every operation must be idempotent. Write `Schema version: 1` last, only after all required work and verification succeed. An interruption must leave a safe retry.
- Schema versions are independent of product release numbers.

### Required snapshot before directory mutation

Before any migration changes an existing `coaching_state/` directory—including reconstructing its index or adding only the version line:

1. Create a new `coaching_state/.snapshots/pre-schema-v[target]-[timestamp]/` directory. Never include `.snapshots/` itself in a snapshot.
2. Copy every existing top-level state file byte-for-byte into it before modifying a source file.
3. Write a snapshot manifest listing each source path, byte count, and SHA-256 hash.
4. Verify the copied-file inventory, byte counts, and hashes against the sources. If verification fails, stop without changing live state.
5. Keep the verified snapshot. Normal command routing ignores `.snapshots/`; it exists only for recovery.

Do not reuse or overwrite an earlier snapshot. A retry creates a new one. If a later migration step fails, leave the schema version unchanged and restore from the verified snapshot before retrying if any partial edit cannot be proven safe.

## Version 1 Adoption for Existing Split State

If `coaching_state/` already exists, adopt it without bulk migration:

1. Verify that its existing Markdown files are readable. If both the directory and legacy `coaching_state.md` exist, do not merge or replace either automatically. Ask which is authoritative, then complete one explicit branch so the gate does not recur:
   - **Split directory is authoritative:** create and verify the directory snapshot below; record the monolith byte count/hash; rename the monolith to a unique `coaching_state.md.pre-split-backup-[timestamp]` and verify its hash. Continue at step 3 using that verified snapshot; do not create a redundant second snapshot. Never delete the backup.
   - **Monolith is authoritative:** create and verify the directory snapshot below. Confirm it contains every existing top-level state file, then remove only those verified top-level copies from the active directory while preserving `.snapshots/` and `archive/cycles/`. Skip the remaining Version 1 Adoption steps and run the Monolith to Directory Migration into the now-empty active top level. Its final monolith rename removes the recurring gate; never delete either backup.
   - **Candidate wants a merge:** stop automatic migration. Snapshot/hash both sources, choose a primary, then reconcile one section or stable-keyed record at a time under the State Write Contract. Preserve conflicts verbatim for candidate resolution; never concatenate duplicate tables or guess which value wins. Write the version only after the merged state validates and rename the monolith to a verified backup.
2. Create and verify the required snapshot unless step 1 already created it for the split-authoritative branch.
3. If `index.md` is absent, reconstruct only the index and Quick Context from available facts. Do not infer candidate facts; use `unknown` for unavailable Quick Context values. Omit the version line for now.
4. Normalize only root/index structures required for routing:
   - Rename the Quick Context key `Next interviews` to canonical `Next interview`, preserving its value verbatim.
   - Ensure Quick Context has one `Interview timeline` key. Copy an unambiguous date from Profile when available; map semantic aliases such as `Active now` or `current` to `ongoing`; otherwise use `unknown`.
   - Ensure the Files manifest points to every existing top-level state file. Preserve additional files and manifest entries.
   - Preserve the existing canonical `Status` value. If duplicate or conflicting root `Status` fields exist, do not guess: preserve their text and resolve the conflict before version adoption.
5. Do **not** add missing Profile, Calibration, Asset, Intelligence, Storybank, Score, or Interview Loop fields. Do not rename historical table columns merely to match current templates. Readers must accept legacy aliases; a command may bring the specific record it is already updating to the current format.
6. Verify that all pre-existing top-level state files still exist and that files not intentionally normalized retain their pre-migration hashes.
7. Write `Schema version: 1` to `index.md` last and verify that exactly one version line exists.

This adoption is silent unless an ambiguous root conflict requires the candidate's input or affects the immediate recommendation.

## Monolith to Directory Migration

If `coaching_state.md` exists as a single file and no `coaching_state/` directory exists—or it was selected as authoritative and the existing directory's verified top-level files were preserved under `.snapshots/` as described above:

1. Record the source file's byte count and SHA-256 hash.
2. Create the `coaching_state/` directory if absent; if the dual-source branch already left a verified, empty active top level, reuse it while preserving `.snapshots/` and `archive/cycles/`.
3. Parse the monolith by `## ` headers and split sections using this mapping:
   - `## Profile`, `## Resume Analysis`, `## Active Coaching Strategy`, `## Calibration State`, `## Drill Progression` → `profile.md`
   - `## Storybank` (including `### Story Details`) → `storybank.md`
   - `## Interview Loops` and `## Outcome Log` → `interviews.md`
   - `## Interview Intelligence` → `intelligence.md`
   - `## Score History` → `scores.md`
   - `## Session Log`, `## Meta-Check Log`, `## Coaching Notes` → `tracking.md`
   - `## Scout Config`, `## Scout Opportunities` → `opportunities.md`
   - all `## JD Analysis:` sections and `### Past JD Analyses` → `jd_analyses.md`
   - LinkedIn, Resume, Positioning, Outreach, Comp, and Presentation sections → `assets.md`
   - unrecognized `## ` sections → `tracking.md` under `## Preserved Unrecognized State`, verbatim
   - all content before the first `## ` heading, including unknown root metadata, comments, or prose → `tracking.md` under `## Preserved Legacy Preamble`, verbatim
4. Generate `index.md` from `references/state-schemas.md`, deriving only known Quick Context values and using `unknown` otherwise. Omit its version line.
5. If root `opportunities_bad_fit.md` exists, copy it to `coaching_state/opportunities_bad_fit.md` and verify byte count and hash. Then rename the source to a timestamped `.pre-split-backup`; never delete it and never overwrite an existing backup.
6. Verify that every source section occurs verbatim in exactly one destination, all generated files are readable, and table-row counts match the source.
7. Rename `coaching_state.md` to `coaching_state.md.pre-split-backup`; verify its byte count and hash match the recorded source. Never overwrite an existing backup—use a timestamped backup name instead.
8. Add a migration note to Coaching Notes, then write `Schema version: 1` last.

The monolith backup is the recovery copy and must not be deleted automatically. After a successful split, missing current-template fields remain unknown and are populated only when their records are naturally updated.
