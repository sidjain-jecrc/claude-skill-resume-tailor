# Multi-Job Resume Tailoring Workflow

## Overview

Handles 3-5 similar jobs efficiently by consolidating experience discovery while maintaining per-job research depth.

**Architecture:** Shared Discovery + Per-Job Tailoring

**Target Use Case:**
- Small batches (3-5 jobs)
- Moderately similar roles (60%+ requirement overlap)
- Continuous workflow (add jobs incrementally)

**Time Savings:**
- 3 jobs: ~40 min (vs 45 min sequential) = 11% savings
- 5 jobs: ~55 min (vs 75 min sequential) = 27% savings

**Sub-files:**
- `multi-job-discovery.md` - Phase 2: Shared experience discovery
- `multi-job-processing.md` - Phase 3-4: Per-job processing and batch finalization
- `multi-job-advanced.md` - Incremental batch support and error handling

---

## Phase 0: Job Intake & Batch Initialization

**Goal:** Collect all job descriptions and initialize batch structure.

**User Interaction:**
Offer three input methods: paste all now, one at a time, or provide URLs.

**For each job collect:**
- Job description (text or URL)
- Company name (extract from JD if possible)
- Role title (extract from JD if possible)
- Priority (high/medium/low, default: medium)
- Optional notes (e.g., "referral from X")

**Quick JD Parsing** (lightweight, NOT full research):
Extract must-have requirements, nice-to-have requirements, technical skills, soft skills, and domain areas. Purpose: identify gaps for discovery phase.

**Batch Directory Structure:**
```
resumes/batches/batch-{YYYY-MM-DD}-{slug}/
├── _batch_state.json          # State tracking
├── _aggregate_gaps.md         # Gap analysis (Phase 1)
├── _discovered_experiences.md # Discovery output (Phase 2)
└── (job directories created during per-job processing)
```

**Initialize `_batch_state.json`** with batch_id, created timestamp, current_phase, processing_mode, and jobs array (each with job_id, company, role, jd_text, priority, notes, status, requirements, gaps).

**Library Initialization:** Run standard Phase 0 from SKILL.md once for the entire batch.

**Checkpoint:** Present batch summary and confirm complete before proceeding.

---

## Phase 1: Aggregate Gap Analysis

**Goal:** Build unified gap list across all jobs to guide single efficient discovery session.

**1.1 Extract Requirements from All JDs:**
For each job, parse requirements (from Phase 0 quick parse), categorize must-have vs nice-to-have, extract keywords and skill areas.

**1.2 Build Requirement Matrix:**
Create a matrix: requirements (rows) x jobs (columns). For each requirement, check which jobs need it and how well the current library matches.

**1.3 Deduplicate and Prioritize:**
Group similar requirements across jobs. Classify as:
- **Critical (3+ jobs):** High-leverage gaps, address first
- **Important (2 jobs):** Medium-leverage gaps
- **Job-specific (1 job):** Low-leverage, address last

**1.4 Calculate Coverage:**
For each job, match library content against requirements. Score using matching-strategies.md criteria.

**1.5 Generate Aggregate Gap Report:**
Save to `_aggregate_gaps.md` with:
- Coverage summary per job (percentage)
- Critical gaps (appear in 3+ jobs) with current confidence
- Important gaps (appear in 2 jobs)
- Job-specific gaps
- Aggregate statistics (total unique gaps, overlap percentage)
- Recommended discovery time estimate

**Present to User:**
Show aggregate gap analysis with per-job coverage, gap breakdown by priority, and estimated discovery time.

**Options offered:**
1. Start discovery session (recommended)
2. Skip discovery, proceed with current library
3. Review detailed gap analysis first

**Checkpoint:** User chooses next action before proceeding.

---

## Next Steps

- **Phase 2 (Shared Discovery):** See `multi-job-discovery.md`
- **Phase 3-4 (Processing + Finalization):** See `multi-job-processing.md`
- **Incremental Batches + Error Handling:** See `multi-job-advanced.md`
