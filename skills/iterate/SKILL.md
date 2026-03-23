# /iterate — Measure, Learn, Improve

A feedback loop skill that measures actual output quality after an agent completes work.
The goal: did the code compile? Does the game run? Did it break anything?

## The Iteration Loop

```
Implement → Verify → Measure → Learn → Improve
     ↑                                    │
     └────────────────────────────────────┘
```

## Phase 1: VERIFY (Does it work?)

```bash
# 1. TypeScript compiles?
cd games/GAME_NAME && npx tsc --noEmit
# Result: PASS/FAIL + error count

# 2. Game builds?
cd games/GAME_NAME && npx vite build
# Result: PASS/FAIL + bundle size

# 3. No regressions? (if tests exist)
cd games/GAME_NAME && npx vitest run 2>/dev/null
# Result: PASS/FAIL + test count

# 4. Game loads in browser? (if Playwright available)
# npx playwright test --project=chromium
```

## Phase 2: MEASURE (Quality metrics)

Collect these metrics after every task completion:

```json
{
  "taskId": "task_xxx",
  "agentId": "agent_xxx",
  "metrics": {
    "compiles": true,
    "builds": true,
    "bundleSize": 342666,
    "testsPassing": 5,
    "testsFailing": 0,
    "typeErrors": 0,
    "lintWarnings": 2,
    "filesChanged": 3,
    "linesAdded": 120,
    "linesRemoved": 15,
    "durationSeconds": 1800
  }
}
```

## Phase 3: LEARN (Extract patterns)

After measuring, automatically:
1. Record metrics to performance tracking API
2. If build failed → create a fix task
3. If tests failed → create a regression task
4. If everything passed → record success pattern as a learning
5. Compare against previous iterations — is quality improving?

```bash
# Record performance
pajama performance record --agent AGENT_ID --type code --duration 1800 --ci-passed true

# Record learning
pajama learning create -c pattern -t "What worked" --content "Details..."
```

## Phase 4: IMPROVE (Adjust approach)

Based on accumulated metrics:
- If an agent's CI pass rate < 80% → adjust task complexity (smaller tasks)
- If bundle size growing > 10% per task → flag for architect review
- If same file edited by multiple tasks → merge into one task next time
- If task duration > 4h → decompose into subtasks

## When to Run

Run /iterate after EVERY task completion. Make it automatic:
1. Agent completes task → /iterate runs
2. Metrics collected → stored in API
3. Patterns extracted → stored as learnings
4. Dashboard updated → visible to all agents
