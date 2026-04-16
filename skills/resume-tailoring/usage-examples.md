# Usage Examples

## Example 1: Internal Role (Same Company)
```
USER: "I want to apply for Principal PM role in 1ES team at Microsoft.
      Here's the JD: {paste}"

SKILL:
1. Library Build: Finds 29 resumes
2. Research: Microsoft 1ES team, internal culture, role benchmarking
3. Template: Features PM2 Azure Eng Systems role (most relevant)
4. Discovery: Surfaces VS Code extension, Bhavana AI side project
5. Assembly: 92% JD coverage, 75% direct matches
6. Generate: MD + DOCX + Report
7. User approves -> Library updated with new resume + 6 discovered experiences

RESULT: Highly competitive application leveraging internal experience
```

## Example 2: Career Transition (Different Domain)
```
USER: "I'm a TPM trying to transition to ecology PM role. JD: {paste}"

SKILL:
1. Library Build: Finds existing TPM resumes
2. Research: Ecology sector, sustainability focus, cross-domain transfers
3. Template: Reframes "Technical Program Manager" -> "Program Manager,
             Environmental Systems" emphasizing systems thinking
4. Discovery: Surfaces volunteer conservation work, graduate research in
             environmental modeling
5. Assembly: 65% JD coverage - flags gaps in domain-specific knowledge
6. Generate: Resume + gap analysis with cover letter recommendations

RESULT: Bridges technical skills with environmental domain
```

## Example 3: Career Gap Handling
```
USER: "I have a 2-year gap while starting a company. JD: {paste}"

SKILL:
1. Library Build: Finds pre-gap resumes
2. Research: Standard analysis
3. Template: Includes startup as legitimate role
4. Discovery: Surfaces skills developed during startup (fundraising,
             product development, team building)
5. Assembly: Frames gap as entrepreneurial experience
6. Generate: Resume presenting gap as valuable experience

RESULT: Gap becomes strength showing initiative and diverse skills
```

## Example 4: Multi-Job Batch (3 Similar Roles)
```
USER: "I want to apply for these 3 TPM roles:
      1. Microsoft 1ES Principal PM
      2. Google Cloud Senior TPM
      3. AWS Container Services Senior PM
      Here are the JDs: {paste 3 JDs}"

SKILL:
1. Multi-job detection: Triggered (3 JDs detected)
2. Intake: Collects all 3 JDs, initializes batch
3. Library Build: Finds 29 resumes (once)
4. Gap Analysis: Identifies 14 gaps, 8 unique after deduplication
5. Shared Discovery: 30-minute session surfaces 5 new experiences
   - Kubernetes CI/CD for nonprofits
   - Azure migration for university lab
   - Cross-functional team leadership examples
   - Recent hackathon project
   - Open source contributions
6. Per-Job Processing (x3):
   - Job 1 (Microsoft): 85% coverage, emphasizes Azure/1ES alignment
   - Job 2 (Google): 88% coverage, emphasizes technical depth
   - Job 3 (AWS): 78% coverage, addresses AWS gap in cover letter recs
7. Batch Finalization: All 3 resumes reviewed, approved, added to library

RESULT: 3 high-quality resumes in 40 minutes vs 45 minutes sequential
        5 new experiences captured, available for future applications
        Average coverage: 84%, all critical gaps resolved
```

## Example 5: Incremental Batch Addition
```
WEEK 1:
USER: "I want to apply for 3 jobs: {Microsoft, Google, AWS}"
SKILL: [Processes batch as above, completes in 40 min]

WEEK 2:
USER: "I found 2 more jobs: Stripe and Meta. Add them to my batch?"
SKILL:
1. Load existing batch (includes 5 previously discovered experiences)
2. Intake: Adds Job 4 (Stripe), Job 5 (Meta)
3. Incremental Gap Analysis: Only 3 new gaps (vs 14 original)
   - Payment systems (Stripe-specific)
   - Social networking (Meta-specific)
   - React/frontend (both)
4. Incremental Discovery: 10-minute session for new gaps only
   - Surfaces payment processing side project
   - React work from bootcamp
   - Large-scale system design course
5. Per-Job Processing (x2): Jobs 4, 5 processed independently
6. Updated Batch Summary: Now 5 jobs total, 8 experiences discovered

RESULT: 2 additional resumes in 20 minutes (vs 30 min if starting from scratch)
        Time saved by not re-asking 8 previous gaps: ~20 minutes
```
