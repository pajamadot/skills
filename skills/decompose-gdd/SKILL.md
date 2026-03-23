# /decompose-gdd — Parse GDD into Task DAG

Read a Game Design Document and create a dependency-aware task graph
in the coordination API.

## Process

1. Find the GDD: `cat games/*/GDD.md`
2. Extract all features (checklist items `- [ ]`)
3. For each feature:
   - Determine task type (code, art, test, design)
   - Set priority (core mechanics=10, features=7, polish=4)
   - Identify dependencies (what must be done first?)
   - List required capabilities
   - Write a goal-oriented description (WHAT not HOW)

4. Create tasks via API in dependency order:
   ```bash
   # First: tasks with no dependencies
   curl -X POST $API/tasks/create -H "Content-Type: application/json" \
     -d '{"title":"...","type":"code","priority":10,"gameId":"...","dependsOn":[]}'

   # Then: tasks that depend on the first batch
   curl -X POST $API/tasks/create -H "Content-Type: application/json" \
     -d '{"title":"...","type":"code","priority":7,"gameId":"...","dependsOn":["task_xxx"]}'
   ```

5. Broadcast to agents:
   ```bash
   curl -X POST $API/messages/broadcast -H "Content-Type: application/json" \
     -d '{"fromAgent":"orchestrator","subject":"Tasks ready","body":"X tasks created for [game]. Priority: [what to work on first]."}'
   ```

## Task Decomposition Rules

- Each task: 1-4 hours of work
- Tasks must be independently testable
- Descriptions are GOALS not STEPS
- Core mechanics before features before polish
- Always specify requiredCapabilities
