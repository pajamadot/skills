# /task-next — Find and Claim Next Task

Find the highest-priority available task matching your capabilities and claim it.

## Steps

1. Get your agent config: `cat ~/.pajama-agent.json`
2. Fetch available tasks: `curl -s https://api.pajama.studio/api/v1/tasks/available`
3. Filter tasks matching your capabilities
4. Show the top 3 matches with title, priority, and description
5. Ask which task to claim (or auto-claim the best match)
6. Claim it: `curl -X POST .../tasks/claim -d '{"taskId":"...","agentId":"..."}'`
7. Create the git branch: `git checkout -b task/TASK_ID`
8. Read relevant shared memory and learnings for context
9. Show the task description and suggested approach
