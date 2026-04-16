---
name: resume-tailoring
description: Tailors resumes for job applications. Researches company/role, creates optimized templates, conducts branching experience discovery to surface undocumented skills, and generates professional multi-format resumes from user's resume library while maintaining factual integrity.
when_to_use: When user provides a job description and wants a tailored resume, asks to optimize a resume for a specific role, mentions applying for a job, or wants help surfacing undocumented experiences for a job application.
argument-hint: "[job description text or URL]"
allowed-tools: Read Glob Grep Write WebSearch WebFetch
---

# Resume Tailoring Skill

## Overview

Generates high-quality, tailored resumes optimized for specific job descriptions while maintaining factual integrity. Builds resumes around the holistic person by surfacing undocumented experiences through conversational discovery.

**Core Principle:** Truth-preserving optimization - maximize fit while maintaining factual integrity. Never fabricate experience, but intelligently reframe and emphasize relevant aspects.

**Mission:** A person's ability to get a job should be based on their experiences and capabilities, not on their resume writing skills.

## When to Use

Use this skill when:
- User provides a job description and wants a tailored resume
- User has multiple existing resumes in markdown format
- User wants to optimize their application for a specific role/company
- User needs help surfacing and articulating undocumented experiences

**DO NOT use for:**
- Generic resume writing from scratch (user needs existing resume library)
- Cover letters (different skill)
- LinkedIn profile optimization (different skill)

## Quick Start

**Required from user:**
1. Job description (text or URL)
2. Resume library location (defaults to `resumes/` in current directory)

**Single-Job Workflow:**
1. Build library from existing resumes
2. Research company/role
3. Create template (with user checkpoint)
4. Optional: Branching experience discovery
5. Match content with confidence scoring
6. Generate MD + DOCX + PDF + Report
7. User review -> Optional library update

## Supporting Files

- `research-prompts.md` - Structured prompts for company/role research
- `matching-strategies.md` - Content matching algorithms and scoring
- `branching-questions.md` - Experience discovery conversation patterns
- `multi-job-workflow.md` - Multi-job batch overview, intake, and gap analysis
- `multi-job-discovery.md` - Shared experience discovery for multi-job batches
- `multi-job-processing.md` - Per-job processing and batch finalization
- `multi-job-advanced.md` - Incremental batch support and error handling
- `error-handling.md` - Edge cases and graceful degradation
- `usage-examples.md` - Detailed workflow examples
- `testing-guidelines.md` - Manual testing checklist

---

## Multi-Job Detection

**Triggers when user provides:**
- Multiple JD URLs (comma or newline separated)
- Phrases: "multiple jobs", "several positions", "batch", "3 jobs"
- List of companies/roles: "Microsoft PM, Google TPM, AWS PM"

**If detected**, offer batch mode with shared experience discovery. Benefits:
- Single discovery session covers all gaps (ask once, apply to all)
- Aggregate gap analysis with deduplication across jobs
- 11-27% time savings over sequential processing

**If user confirms:** Use `multi-job-workflow.md` for complete workflow.
**If user declines or single job:** Use the single-job workflow below (Phase 0 onwards).

---

## Phase 0: Library Initialization

**Always runs first - builds fresh resume database.**

1. **Locate resume directory:** User provides path OR default to `./resumes/`
2. **Scan for markdown files:** Use Glob tool with `*.md` pattern
3. **Parse each resume:** Use Read tool to extract roles, bullets, skills, education
4. **Build experience database:**
   - Roles with company, title, dates, bullets
   - Skills categorized as technical, product, leadership
   - Education entries
   - User preferences (typical length, section order, bullet style)
5. **Tag content automatically:**
   - Themes: leadership, technical, analytics, etc.
   - Metrics: numbers, percentages, dollar amounts
   - Keywords: frequent technical terms, action verbs

**Output:** In-memory database ready for matching.

---

## Phase 1: Research Phase

**Goal:** Build comprehensive "success profile" beyond just the job description.

**1.1 Job Description Parsing:**
Use `research-prompts.md` JD parsing template. Extract requirements, keywords, implicit preferences, red flags, role archetype.

**1.2 Company Research:**
WebSearch for company mission/values/culture, engineering blog, recent news, team structure. Synthesize into company profile.

**1.3 Role Benchmarking:**
WebSearch LinkedIn profiles for similar roles. Analyze common backgrounds, skills, terminology.

**1.4 Success Profile Synthesis:**
Combine all research into structured profile including:
- Core requirements (must-have) and valued capabilities (nice-to-have)
- Cultural fit signals and narrative themes
- Terminology map (user's background -> their language)
- Risk factors + mitigations

**Checkpoint:** Present success profile to user for validation before proceeding.

**Output:** Validated success profile document.

---

## Phase 2: Template Generation

**Goal:** Create resume structure optimized for this specific role.

**2.1 Analyze Resume Library:**
Extract all roles, titles, companies, date ranges. Identify role archetypes and experience clusters.

**2.2 Role Consolidation Decision:**
- **Consolidate when:** Same company, similar responsibilities, combined narrative stronger
- **Keep separate when:** Different companies (ALWAYS), dramatically different responsibilities, specific progression story matters
- Present options A (consolidated) and B (separate) with rationale

**2.3 Title Reframing Principles:**
Stay truthful to what you did, emphasize the aspect most relevant to target.
- Emphasize different aspects of the same role
- Use industry-standard terminology
- Add specialization when truthful
- Adjust seniority indicators based on scope

**Constraints:** NEVER claim work you didn't do. NEVER inflate seniority beyond defensible. Company name and dates MUST be exact.

**2.4 Generate Template Structure:**
Build markdown template with guidance for each section: Professional Summary, Key Skills, Professional Experience (with bullet allocation per role), Education, Optional Sections.

**Checkpoint:** Present template to user showing structure, consolidation decisions, title reframing, and bullet allocation. Wait for approval.

**Output:** Approved template skeleton with guidance for each section.

---

## Phase 2.5: Experience Discovery (OPTIONAL)

**Goal:** Surface undocumented experiences through conversational discovery.

**Trigger:** After template approval, if gaps identified. Offer structured brainstorming session (typically 10-15 minutes). User can accept or skip.

**Branching Interview Process** (see `branching-questions.md` for full patterns):

1. **Open probe** for each gap (technical, soft skill, or recent work)
2. **Branch based on answer:** YES -> deep dive | INDIRECT -> explore transferability | ADJACENT -> explore related | NO -> try broader category
3. **Follow-up systematically:** what, how, why, metrics, context, validation
4. **Capture immediately:** Document as resume bullet, tag which gaps addressed

**Integration:** For each discovered experience, user chooses: Add to current resume, Add to library only, Refine further, or Discard.

**Important:** Keep truthfulness bar high. Focus on gaps and weak matches. Time-box if needed. Recognize when to move on.

**Output:** New experiences integrated into library, ready for matching.

---

## Phase 3: Assembly Phase

**Goal:** Fill approved template with best-matching content, with transparent scoring.

**3.1 For Each Template Slot:**

1. Extract all candidate bullets from library + discovered experiences
2. Score each candidate using `matching-strategies.md`:
   - Direct match (40%): Keywords, domain, technology, outcome
   - Transferable (30%): Same capability, different context
   - Adjacent (20%): Related tools, methods, problem space
   - Impact (10%): Achievement type alignment
3. Rank by confidence band: DIRECT (90-100%), TRANSFERABLE (75-89%), ADJACENT (60-74%), WEAK/GAP (<60%)
4. Present top 3 matches with analysis for each slot

**3.2 Handle Gaps (confidence <60%):**
Show best available match. Offer options: reframe (show before/after with truthfulness rationale), acknowledge in cover letter, omit slot, or use best available.

**3.3 Content Reframing:**
When good match but terminology misaligned, apply strategies from `matching-strategies.md`. Always show before/after with transparency on what changed and why.

**Checkpoint:** Present complete coverage summary (direct/transferable/adjacent/gap percentages), reframings applied, gaps identified, and overall JD coverage percentage. Wait for approval.

**Output:** Complete bullet-by-bullet mapping with confidence scores and reframings.

---

## Phase 4: Generation Phase

**Goal:** Create professional multi-format outputs.

**4.1 Markdown Generation:**
Compile mapped content into clean markdown following user's preferences (formatting style, bullet structure, section ordering, typical length). Output: `{Name}_{Company}_{Role}_Resume.md`

**4.2 DOCX Generation:**
Use `document-skills:docx` sub-skill with professional fonts (Calibri 11pt), proper spacing, clean bullet formatting, header with contact info, appropriate margins. Output: `{Name}_{Company}_{Role}_Resume.docx`

**4.3 PDF Generation (Optional):**
If requested, use `document-skills:pdf` sub-skill. Output: `{Name}_{Company}_{Role}_Resume.pdf`

**4.4 Generation Summary Report:**
Create metadata file with: target role summary, success profile summary, content mapping summary (match percentages), reframings applied, source resumes used, gaps before/after discovery, key differentiators, and interview prep recommendations.
Output: `{Name}_{Company}_{Role}_Resume_Report.md`

**Present to user** with quality metrics (JD coverage, direct match %, newly discovered experiences).

---

## Phase 5: Library Update (CONDITIONAL)

**After user reviews generated resume, offer three options:**

1. **Save to library** - Move files to library directory, rebuild database, preserve generation metadata, announce updated library stats
2. **Need revisions** - Collect feedback, make changes, re-present for approval
3. **Save but don't add to library** - Keep files in current directory only

**Benefits of library update:** Grows library with each resume, new bullet variations become available, reframings that work can be reused, discovered experiences permanently captured.

---

## Error Handling

See `error-handling.md` for detailed edge case handling including:
- Insufficient resume library (1-2 resumes)
- No good matches (confidence <60%)
- Research phase failures
- Job description quality issues
- Ambiguous role consolidation
- Resume length constraints

**General principles:**
- All checkpoints allow going back to previous phase
- Generation failures fall back to markdown-only
- Research limited -> fall back to JD-only analysis
- Library small -> emphasize discovery phase
- Matches weak -> transparent gap identification

---

## Examples & Testing

- See `usage-examples.md` for detailed workflow examples (internal roles, career transitions, career gaps, multi-job batches)
- See `testing-guidelines.md` for manual testing checklist and regression testing procedures
