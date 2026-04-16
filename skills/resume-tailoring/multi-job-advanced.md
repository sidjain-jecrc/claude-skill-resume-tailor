# Multi-Job: Incremental Batches & Error Handling

## Incremental Batch Support

**Goal:** Add new jobs to existing batches without re-doing completed work.

**Scenario:** User processes 3 jobs today, finds 2 more jobs next week.

### Detect Add Request

Triggers when user says: "Add another job to my batch", "I found 2 more jobs", "Resume batch {batch_id} and add jobs".

### Load Existing Batch

Load batch state. If batch is completed, reopen for new jobs. Show existing completed jobs and prompt for new job details.

### Intake New Jobs

Same collection process as Phase 0, but append to existing batch. Continue job numbering (job-4, job-5, etc.).

### Incremental Gap Analysis

- Compare new job requirements against enriched library (includes previous discoveries)
- Identify only NEW gaps not covered by previous sessions
- Show what's already covered from previous batch
- Estimate reduced discovery time

**Key benefit:** Previously discovered experiences carry forward. Typical result: 3 new gaps vs 14 original, ~10 min discovery vs ~30 min.

### Incremental Discovery

Only ask about NEW gaps. Do not re-ask questions already answered in previous sessions. Use same branching interview process from `multi-job-discovery.md`.

### Process New Jobs

Run Phase 3 (per-job processing) for new jobs only. Existing completed jobs are untouched.

### Update Batch Summary

Append new jobs to `_batch_summary.md` with incremental addition date, new job details, and updated statistics (total jobs, incremental discoveries, cumulative discoveries).

---

## Error Handling & Edge Cases

### Edge Case 1: Jobs Are More Diverse Than Expected

**Detection:** During gap analysis, <40% gap overlap between jobs.

**Handling:** Recommend splitting into sub-batches by similarity. Options:
1. Split into batches (recommended)
2. Continue with unified discovery (will take longer)
3. Remove dissimilar jobs

### Edge Case 2: Discovery Reveals Experience Relevant to Only 1 Job

**Handling:** Tag experience as job-specific. Offer to explore broader category (e.g., if Azure-specific Kubernetes, explore general container orchestration concepts that transfer across providers).

### Edge Case 3: One Job's Research Fails

**Handling:** Fall back to JD-only analysis for that job. Options:
1. Continue with JD-only (recommended)
2. Skip job, process others first
3. User provides context manually
4. Remove from batch

**Principle:** Don't let one failure block the entire batch.

### Edge Case 4: User Wants to Add/Remove Jobs Mid-Process

**Add:** Collect new job details. Run quick gap check. If new gaps exist, do incremental discovery. Then process normally.

**Remove:** Archive job files (don't delete). Keep discovered experiences in library. Continue with remaining jobs.

### Edge Case 5: Library Update Conflicts

**Scenario:** User approves some jobs, rejects others, wants to revise rest.

**Options:**
1. Individual approval (recommended) - add approved jobs now, handle others separately
2. Batch approval - wait until all jobs finalized
3. Selective approval - choose which jobs and experiences to integrate

### Edge Case 6: Batch Processing Interrupted

**Auto-save** after each major milestone (job completion, discovery phase, gap analysis, user checkpoints).

**Resume:** User says "resume batch {batch_id}" or "continue my batch". Pick up exactly where left off using saved batch state.

### Edge Case 7: No Gaps Found

**Scenario:** All jobs well-covered by existing library.

**Options:**
1. Skip discovery, proceed to per-job processing (recommended)
2. Optional discovery anyway
3. Review what small gaps exist

### Error Recovery Principles

1. **Never lose progress:** Auto-save batch state frequently
2. **Partial success is success:** Some jobs completing is better than none
3. **Transparent failures:** Always explain what went wrong and options
4. **Graceful degradation:** Fall back to JD-only, single-job mode, or skip
5. **User control:** Always provide options, never force a path

### Graceful Degradation Paths

- Research fails -> Fall back to JD-only analysis
- Library too small -> Emphasize discovery phase
- WebSearch unavailable -> Use cached data or skip research
- DOCX generation fails -> Provide markdown only
- One job fails -> Continue with others, revisit failed job later
