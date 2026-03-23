# /start — Project Onboarding

Detect the current project state and guide the user to the right next step.

## Steps

1. Check if the user is registered as an agent:
   - Run `cat ~/.pajama-agent.json` to check
   - If not registered, guide them through `pajama agent register`

2. Check the coordination API:
   - `curl -s https://api.pajama.studio/api/v1/agents/active`
   - `curl -s https://api.pajama.studio/api/v1/tasks/available`
   - `curl -s https://api.pajama.studio/api/v1/games`

3. Check git state:
   - `git branch --show-current`
   - `git log --oneline -5`
   - Any uncommitted changes?

4. Based on state, recommend:
   - New user → register and read CLAUDE.md
   - No games → create a game project
   - Games but no tasks → decompose GDD into tasks
   - Tasks available → claim one and start working
   - Already on a task branch → continue working
   - Task complete → create PR and mark done

5. Show a brief status summary of the whole studio.
