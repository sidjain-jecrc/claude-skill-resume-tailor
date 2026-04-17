# Testing Guidelines

## Manual Testing Checklist

### Test 1: Happy Path
```
- Provide JD with clear requirements
- Library with 10+ resumes
- Run all phases without skipping
- Verify generated files
- Check library update
PASS CRITERIA:
- All files generated correctly
- JD coverage >70%
- No errors in any phase
```

### Test 2: Minimal Library
```
- Provide only 2 resumes
- Run through workflow
- Verify gap handling
PASS CRITERIA:
- Graceful warning about limited library
- Still produces reasonable output
- Gaps clearly identified
```

### Test 3: Research Failures
```
- Use obscure company with minimal online presence
- Verify fallback to JD-only
PASS CRITERIA:
- Warning about limited research
- Proceeds with JD analysis
- Template still reasonable
```

### Test 4: Experience Discovery Value
```
- Run with deliberate gaps in library
- Conduct experience discovery
- Verify new experiences integrated
PASS CRITERIA:
- Discovers genuine undocumented experiences
- Integrates into final resume
- Improves JD coverage
```

### Test 5: Title Reframing
```
- Test various role transitions
- Verify title reframing suggestions
PASS CRITERIA:
- Multiple options provided
- Truthfulness maintained
- Rationales clear
```

### Test 6: Multi-format Generation
```
- Generate MD, DOCX, PDF, Report
- Verify formatting consistency
PASS CRITERIA:
- All formats readable
- Formatting professional
- Content identical across formats
```

## Regression Testing
```
After any SKILL.md changes:
1. Re-run Test 1 (happy path)
2. Verify no functionality broken
3. Commit only if passes
```

## Multi-Job Testing

See `multi-job-test-checklist.md` for comprehensive multi-job test cases covering:
- Happy path (3 similar jobs)
- Diverse jobs (low overlap detection)
- Incremental batch addition
- Pause/resume functionality
- Individual vs batch review
- Express mode processing
- Error handling and graceful degradation
