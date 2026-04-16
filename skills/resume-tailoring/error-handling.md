# Error Handling & Edge Cases

## Edge Case 1: Insufficient Resume Library
```
SCENARIO: User has only 1-2 resumes, limited content

HANDLING:
"Limited resume library detected ({N} resumes).

This may result in:
- Fewer matching options
- More gaps in coverage
- Less variety in bullet phrasing

RECOMMENDATIONS:
- Proceed with available content (I'll do my best!)
- Consider adding more resumes after this generation
- Experience Discovery phase will be especially valuable

Continue? (Y/N)"
```

## Edge Case 2: No Good Matches (confidence <60% for critical requirement)
```
SCENARIO: Template slot requires experience user doesn't have

HANDLING:
"GAP: {Requirement}

No matches found with confidence >60%

OPTIONS:
1. Run Experience Discovery - might surface undocumented work
2. Reframe best available ({score}%) - I'll show you the reframing
3. Omit bullet slot - reduce template allocation
4. Note for cover letter - emphasize learning ability

Which approach?"

[Don't force matches - be transparent about gaps]
```

## Edge Case 3: Research Phase Failures
```
SCENARIO: WebSearch fails, LinkedIn unavailable, company info sparse

HANDLING:
"Limited company research available.

What I found:
- {Available info}

What's missing:
- {Missing areas}

Falling back to job description-only analysis.
Result: Template will be optimized for JD but may miss cultural nuances.

Do you have additional context about:
- Company culture?
- Team structure?
- Technologies used?

(Optional - you can share or skip)"

[Proceed with best-effort approach]
```

## Edge Case 4: Job Description Quality Issues
```
SCENARIO: Vague JD, missing requirements, poorly written

HANDLING:
"Job description lacks detail in areas:
- {Missing area 1}
- {Missing area 2}

This may limit template optimization.

Do you have additional context about:
- {Question 1}
- {Question 2}

(Optional - I'll work with what's available)"

[Extract what's possible, proceed]
```

## Edge Case 5: Ambiguous Role Consolidation
```
SCENARIO: Unclear whether to merge roles or keep separate

HANDLING:
"Ambiguous consolidation decision for {Company}

OPTION A (Consolidated): {Rationale}
OPTION B (Separate): {Rationale}

Both are defensible. Which do you prefer?

(This becomes your preference for similar situations)"

[Remember preference for future]
```

## Edge Case 6: Resume Length Constraints
```
SCENARIO: Too much good content, exceeds 2 pages

HANDLING:
"Content exceeds 2 pages (current: {N} bullets, ~{pages} pages)

PRUNING SUGGESTIONS (ranked by relevance):
Remove:
- {Bullet X}: {score}% match (lowest)
- {Bullet Y}: {score}% match
...

Keep all bullets and accept >2 pages?
OR
Remove {N} bullets to fit 2 pages?

Your preference?"

[User decides priority]
```

## Error Recovery

- All checkpoints allow going back to previous phase
- User can request adjustments at any checkpoint
- Generation failures (DOCX/PDF) fall back to markdown-only
- Progress saved between phases (can resume if interrupted)

## Graceful Degradation

- Research limited -> Fall back to JD-only analysis
- Library small -> Work with available + emphasize discovery
- Matches weak -> Transparent gap identification
- Generation fails -> Provide markdown + error details
