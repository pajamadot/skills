# /code-review — Architectural Code Review

Review code changes for architecture, patterns, performance, and correctness.

## Process

1. Identify what to review:
   - If on a task branch: `git diff main...HEAD`
   - If PR specified: `gh pr diff NUMBER`
   - Otherwise: ask what to review

2. Read the changed files and understand the context

3. Check against this checklist:
   - [ ] Follows project conventions (TypeScript strict, Phaser patterns)
   - [ ] No hardcoded gameplay values (should be constants/config)
   - [ ] No performance issues (allocs in hot paths, unnecessary updates)
   - [ ] Code is testable and self-documenting
   - [ ] Matches project architecture (systems/, entities/, scenes/)
   - [ ] No regressions in existing functionality
   - [ ] Edge cases handled
   - [ ] Dependencies are explicit (no implicit ordering)

4. Present findings:
   - **Must fix** — Issues that need resolution
   - **Should fix** — Improvements worth making
   - **Nit** — Style/preference suggestions
   - **Good** — Things done well (positive feedback matters)

5. If everything passes, approve. Otherwise, create follow-up tasks.
