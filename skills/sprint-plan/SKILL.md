# /sprint-plan — Create or Update Sprint Plan

Generate a sprint plan from available tasks in the coordination API.

## Process

1. Fetch current state:
   ```bash
   curl -s https://api.pajama.studio/api/v1/tasks/available
   curl -s https://api.pajama.studio/api/v1/agents/active
   ```

2. Ask user for sprint parameters:
   - Duration (1 week / 2 weeks)
   - Sprint goal (one sentence)
   - Available agent count

3. Select tasks for the sprint:
   - Respect dependency order
   - Match tasks to agent capabilities
   - Don't overcommit (rule of thumb: 3-5 tasks per agent per sprint)

4. Create the sprint plan using the template at
   `.claude/docs/templates/sprint-plan.md`

5. Identify risks:
   - Dependency bottlenecks
   - Capability gaps (no agent for a task type)
   - Tasks with unclear requirements

6. Write the plan to `memory/shared/sprint-current.md`

7. Broadcast sprint start to all agents:
   ```bash
   pajama message broadcast -s "Sprint started" -b "Goal: [goal]. [N] tasks. See memory/shared/sprint-current.md"
   ```
