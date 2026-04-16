# Multi-Job Phase 3-4: Per-Job Processing & Batch Finalization

## Phase 3: Per-Job Processing

**Goal:** Process each job independently through research/template/matching/generation.

**Key Insight:** Once discovery is complete, each job uses the enriched library independently.

### Processing Modes

Before starting, offer user:
1. **INTERACTIVE** (default) - Show checkpoints for each job (template approval, content mapping approval)
2. **EXPRESS** - Auto-approve using best judgment, user reviews all final resumes together

Recommendation: INTERACTIVE for first 1-2 jobs, then switch to EXPRESS.

### Per-Job Loop

For each job (status == "pending"):
1. Set status to "in_progress"
2. Create job directory: `resumes/batches/{batch_id}/job-{N}-{company-slug}/`
3. Process through phases 3A-3D below
4. Set status to "completed"
5. Move to next job

### Phase 3A: Research (Per-Job)

Same depth as SKILL.md Phase 1:
- Company research via WebSearch (mission, values, culture, news)
- Role benchmarking via LinkedIn (3-5 similar role holders)
- Success profile synthesis
- Checkpoint (INTERACTIVE mode): Present success profile for validation

Save to: `job-{N}-{company-slug}/success_profile.md`

EXPRESS mode: Generate profile, save, proceed automatically.

### Phase 3B: Template Generation (Per-Job)

Same process as SKILL.md Phase 2:
- Role consolidation decisions
- Title reframing options
- Bullet allocation
- Checkpoint (INTERACTIVE mode): Approve template structure

Save to: `job-{N}-{company-slug}/template.md`

EXPRESS mode: Generate template using best judgment, proceed automatically.

### Phase 3C: Content Matching (Per-Job)

Same process as SKILL.md Phase 3, using enriched library:
- Match content to template slots
- Confidence scoring (Direct/Transferable/Adjacent)
- Reframing suggestions
- Gap identification (should be minimal after discovery)
- Checkpoint (INTERACTIVE mode): Approve content mapping with coverage summary

Save to: `job-{N}-{company-slug}/content_mapping.md`

EXPRESS mode: Use highest confidence matches, proceed automatically.

### Phase 3D: Generation (Per-Job)

Same process as SKILL.md Phase 4:
- Generate Markdown resume
- Generate DOCX resume (using document-skills:docx)
- Generate Report
- No checkpoint — just generate files

Output files saved to `job-{N}-{company-slug}/`:
- `{Name}_{Company}_{Role}_Resume.md`
- `{Name}_{Company}_{Role}_Resume.docx`
- `{Name}_{Company}_{Role}_Resume_Report.md`

### Progress Tracking

After each job completes, show:
- Quality metrics (JD coverage, direct match %, files generated)
- Jobs remaining and estimated time
- Option to continue, pause, or switch processing mode

### Pause/Resume Support

If user pauses: Save batch state with current progress. User can resume later with "resume batch {batch_id}" or "continue my batch".

---

## Phase 4: Batch Finalization

**Goal:** Present all resumes for review, handle batch-level actions, update library.

### 4.1 Generate Batch Summary

Create `_batch_summary.md` with:
- Job summaries (status, coverage, direct matches, key strengths, remaining gaps, files)
- Batch statistics (discovery impact, coverage metrics, gap resolution)
- Files location directory tree
- Recommendations (interview prep, cover letter focus, application priority based on coverage)

### 4.2 Present to User

Show all job summaries with coverage metrics in a table format. Include batch statistics (experiences discovered, average improvement, time saved).

**Review Options:**
1. **APPROVE ALL** - Save all resumes to library
2. **REVIEW INDIVIDUALLY** - Approve/revise each resume separately
3. **REVISE BATCH** - Make changes across multiple resumes (e.g., "make all summaries shorter", "emphasize leadership more")
4. **SAVE BUT DON'T UPDATE LIBRARY** - Keep files, don't enrich library

### 4.3 Handle Each Option

**Option 1 (Approve All):**
Copy all resume files to library, add discovered experiences to database, tag with metadata, rebuild library indices, update batch state to "completed".

**Option 2 (Review Individually):**
For each job: show JD requirements vs resume coverage, highlight discovered experiences used. User approves, skips, or requests revisions per job.

**Option 3 (Revise Batch):**
Collect revision request. Determine affected jobs. Re-run matching/generation for affected jobs. Re-present for approval. Loop until satisfied.

**Option 4 (Save Without Library Update):**
Save files to batch directory. Preserve batch state for future reference.

### 4.4 Update Final Batch State

Update `_batch_state.json` with completed status, completion timestamp, per-job statuses, and statistics (total_jobs, completed_jobs, new_experiences, average_coverage, total_time_minutes).

---

**Next:** See `multi-job-advanced.md` for incremental batch support and error handling.
