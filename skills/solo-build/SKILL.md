# /solo-build — One Agent Builds the Entire Game

The autonomous single-agent game building loop. One agent claims ALL tasks
for a game and builds it end-to-end, following the same process a team would.

## Prerequisites

- Agent is registered and logged into a workspace
- A game project exists with tasks (from /decompose-gdd)
- Agent has the game repo cloned

## The Loop

```
1. Check available tasks for this game
2. Pick the highest-priority task with met dependencies
3. Claim it (creates git branch automatically)
4. Read related memory, learnings, and architecture decisions
5. Implement the feature
6. Run /iterate (verify: compile, build, test)
7. If verify fails → fix and re-verify (max 3 attempts)
8. Commit and push
9. Mark task done with structured output
10. Record learnings
11. Check if phase gate is met → advance if ready
12. Loop back to step 1
```

## Detailed Steps

### Step 1: Get Tasks
```bash
# Get all available tasks for this game, sorted by priority
curl -s "$API/tasks/available?workspaceId=$WS_ID" | \
  node -e "..." # Filter by gameId, sort by priority, check deps
```

### Step 2: Pick Best Task
Choose the task that:
- Has highest priority
- Has all dependencies completed
- Matches your capabilities (you can do everything as solo agent)

### Step 3: Claim & Branch
```bash
pajama task claim TASK_ID
# Auto-creates: git checkout -b task/TASK_ID
```

### Step 4: Gather Context
```bash
# Read architecture decisions
pajama memory list
pajama learning list --game GAME_ID

# Read the game's CLAUDE.md
cat games/GAME_NAME/CLAUDE.md

# Read existing code to understand patterns
ls games/GAME_NAME/src/
```

### Step 5: Implement
Write the code. Follow these principles:
- Read existing code first, match patterns
- Data-driven values (constants, not magic numbers)
- Each scene/system in its own file
- TypeScript strict mode

### Step 6: Verify (/iterate)
```bash
cd games/GAME_NAME

# Must pass:
npx tsc --noEmit          # Type check
npx vite build             # Build check

# If either fails, fix and retry (max 3 attempts)
```

### Step 7: Commit
```bash
git add -A
git commit -m "feat(GAME_NAME): TASK_TITLE

Implemented: [what you built]
Files: [key files changed]
Tested: [how you verified]"
```

### Step 8: Complete Task
```bash
pajama task done TASK_ID --summary "What I built. Key files: X, Y. Tested: compiles, builds."
```

### Step 9: Record Learning
```bash
pajama learning create \
  -c pattern \
  -t "Short title" \
  --content "What I learned that helps future tasks" \
  --game GAME_ID
```

### Step 10: Check Phase Gate
```bash
# Are all tasks in current phase done?
# If yes, advance to next phase
curl -s "$API/phases/game/GAME_ID"
# If gate requirements met, advance
```

### Step 11: Next Task
Go back to Step 1. Continue until no tasks remain.

## Exit Conditions

- All tasks completed → game is done!
- No tasks available + tasks still in progress → wait (shouldn't happen in solo mode)
- Unresolvable error after 3 retries → create an escalation task and stop

## Key Principle

Even though you're solo, follow the SAME process a team would:
- Still use branches per task
- Still write learnings
- Still check phase gates
- Still record performance metrics

This way, the same game could be built by 5 agents on 5 machines
using the exact same workflow. Solo is just the special case where
one agent does everything.
