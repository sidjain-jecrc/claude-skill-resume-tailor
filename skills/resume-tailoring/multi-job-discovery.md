# Multi-Job Phase 2: Shared Experience Discovery

**Goal:** Surface undocumented experiences across all gaps through a single conversational session.

**Core Principle:** Same branching interview from `branching-questions.md`, but with multi-job context for each question.

---

## Session Flow

### 2.1 Start with Highest-Leverage Gaps

Process gaps in priority order:
1. Critical gaps (appear in 3+ jobs) - 5-7 min each
2. Important gaps (appear in 2 jobs) - 3-5 min each
3. Job-specific gaps - 2-3 min each

### 2.2 Multi-Job Contextualized Questions

For each gap, provide multi-job context before branching interview.

**Single-Job Version (standard):**
> "I noticed the job requires Kubernetes experience. Have you worked with Kubernetes?"

**Multi-Job Version (enhanced):**
> "Kubernetes experience appears in 3 of your target jobs (Microsoft, Google, AWS).
> This is a HIGH-LEVERAGE gap - addressing it helps multiple applications.
> Current best match: 45% confidence ('Deployed containerized app for nonprofit')
> Have you worked with Kubernetes or container orchestration?"

### 2.3 Conduct Branching Interview

For each gap:
1. Initial probe with multi-job context
2. Branch based on answer using `branching-questions.md` patterns:
   - YES -> Deep dive (scale, challenges, metrics)
   - INDIRECT -> Explore role and transferability
   - ADJACENT -> Explore related experience
   - PERSONAL -> Assess recency and substance
   - NO -> Try broader category or move on
3. Follow up systematically: "what," "how," "why," quantify, contextualize, validate
4. Capture immediately with job tags

### 2.4 Capture Structure

Save discoveries to `_discovered_experiences.md`:

For each experience capture:
- **Context:** Where/when, production vs personal
- **Scope:** Scale, duration, impact details
- **Metrics:** Quantified outcomes
- **Addresses gaps in:** Which jobs and which specific gaps
- **Confidence Improvement:** Before/after percentages per gap
- **Bullet Draft:** Achievement-focused resume bullet
- **Integration Decision:** Pending user approval

### 2.5 Track Coverage Improvement in Real-Time

After each discovery, show user:
- Updated coverage percentage per job
- How many critical/important gaps remain
- Ask whether to continue or move on

### 2.6 Integration Decision Per Experience

After discovery session complete, for each experience ask user:
1. **ADD TO LIBRARY FOR ALL JOBS** - Integrate and use everywhere
2. **ADD TO LIBRARY, USE SELECTIVELY** - User picks which jobs
3. **SKIP** - Don't integrate

### 2.7 Enrich Library

For approved experiences:
- Add to library database
- Tag with metadata: discovered_date, addressed_gaps, used_in_jobs, confidence_improvement

### 2.8 Update Batch State

Update `_batch_state.json` with discoveries array containing experience_id, text, context, scope, addresses_jobs, addresses_gaps, confidence_improvement, integrated flag, and bullet_draft.

---

## Output

Present discovery summary:
- New experiences captured and integrated count
- Average coverage improvement
- Final per-job coverage percentages
- Remaining gaps breakdown (critical/important/job-specific)

**Checkpoint:** User approves before moving to per-job processing.

---

**Next:** See `multi-job-processing.md` for Phase 3 (Per-Job Processing) and Phase 4 (Batch Finalization).
