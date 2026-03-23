# /playtest — Structured Playtest Report

Play the game and produce a structured playtest report.

## Process

1. Build and run the game:
   ```bash
   cd games/pajama-runner && pnpm dev
   ```
   (Or navigate to the deployed URL)

2. Play for at least 3 sessions, noting:
   - First impression (0-30 seconds)
   - Core loop feel (30s-2min)
   - Long session (2min+)

3. Record observations in this format:

```markdown
## Playtest Report — [Date]

### Session Summary
- Duration: X minutes
- Sessions: X
- High score: X

### Feel
- Controls: [responsive/sluggish/floaty]
- Difficulty curve: [too easy/good/too hard/unfair]
- Pacing: [too slow/good/too fast]

### Positives
1. [what works well]
2. [what feels satisfying]

### Issues
1. [what feels wrong — specific]
2. [bugs encountered — with repro steps]

### Suggestions
1. [specific improvement with reasoning]
2. [balance adjustment with numbers]
```

4. Write to shared memory:
   ```bash
   pajama learning create -c balance -t "Playtest [date]" --content "[report]"
   ```

5. Create bug tasks for any issues found.
