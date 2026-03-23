# /absorb — Systematic External Project Absorption

A meta-skill for evolving the Pajama Game Studio system by extracting and
integrating the best patterns from external projects.

## Methodology: OODA + TRIZ + Rising Tide

### Phase 1: OBSERVE (What does the external project do?)

```
1. Clone/fetch the repo
2. Read README, architecture docs, CLAUDE.md/AGENTS.md
3. Map the file tree structure
4. Identify the core abstractions (what are their "nouns"?)
5. Identify the key workflows (what are their "verbs"?)
6. Read the most important source files
7. Note what's novel vs what's standard
```

### Phase 2: ORIENT (How does it compare to what we have?)

Use this analysis matrix:

```
| Dimension        | They Do          | We Do           | Gap Type        |
|------------------|------------------|-----------------|-----------------|
| Architecture     | [their approach] | [our approach]  | ADOPT/ADAPT/SKIP|
| Agent model      | ...              | ...             | ...             |
| Task management  | ...              | ...             | ...             |
| Communication    | ...              | ...             | ...             |
| Memory/state     | ...              | ...             | ...             |
| File system      | ...              | ...             | ...             |
| Auth/scoping     | ...              | ...             | ...             |
| CI/CD            | ...              | ...             | ...             |
| Testing          | ...              | ...             | ...             |
| UX/DX            | ...              | ...             | ...             |
```

Gap types:
- **ADOPT**: They have it, we don't, and we should
- **ADAPT**: They have a version, we have a version, theirs is better in specific ways
- **EVOLVE**: Combine both approaches into something better than either
- **SKIP**: They have it but it doesn't fit our architecture
- **AHEAD**: We already have a better solution

### Phase 3: DECIDE (What to absorb?)

Apply TRIZ (Theory of Inventive Problem Solving) principles:
1. **Segmentation** — Can we take just the best part, not the whole thing?
2. **Extraction** — Can we extract the useful mechanism from its context?
3. **Universality** — Does it generalize beyond its original use case?
4. **Nested composition** — Can it layer on top of what we have?
5. **Inversion** — Is the opposite of their approach actually better for us?
6. **Dynamicity** — Is their static approach something we can make dynamic?

For each ADOPT/ADAPT/EVOLVE item, define:
```
What: [specific pattern/feature]
Why: [what problem it solves that we have]
How: [concrete integration plan]
Where: [which files to modify/create]
Risk: [what could break]
```

### Phase 4: ACT (Integrate it)

1. Create/modify files according to the integration plan
2. Typecheck: `npx tsc --noEmit`
3. Deploy: `npx wrangler deploy`
4. Test: `npx tsx tests/e2e/api.test.ts`
5. Record learnings:
   ```bash
   pajama learning create -c decision \
     -t "Absorbed from [repo]: [what]" \
     --content "[what we took, why, how it differs from original]"
   ```

### Phase 5: REFLECT (Did it make us better?)

After integration, verify:
- [ ] Does it fit the Rising Tide principle? (Gets better as models improve?)
- [ ] Is it protocol-stable? (Built on invariant layers?)
- [ ] Does it work distributed? (Multiple machines, not single-session?)
- [ ] E2E tests still pass?
- [ ] Is it documented in CLAUDE.md?

## Anti-Patterns to Avoid

1. **Cargo culting** — Copying code without understanding why
2. **Framework coupling** — Importing their framework as a dependency
3. **Over-absorption** — Taking everything instead of just the 长处
4. **Architecture pollution** — Breaking our clean separation of concerns
5. **Scope creep** — "While we're at it..." additions

## Trigger

Use when:
- Someone shares a repo URL for inspiration
- We discover a competing/complementary project
- We want to evolve a specific subsystem

## Output

After absorption, produce:
1. Analysis matrix (Phase 2)
2. Integration plan (Phase 3)
3. Code changes (Phase 4)
4. Learning record (Phase 5)
