# /balance-check — Analyze Game Balance

Analyze game balance using the designer agent's framework.

## Process

1. Read the game's current constants/config:
   ```bash
   grep -rn "const.*=" games/*/src/ | grep -iE "speed|velocity|gravity|health|damage|rate|interval|chance"
   ```

2. Read existing balance observations:
   ```bash
   curl -s "https://api.pajama.studio/api/v1/learnings/list?category=balance"
   ```

3. Analyze against the balance framework:
   - **Feel knobs**: Are movement/combat/interaction values tuned for game feel?
   - **Curve knobs**: Is the difficulty ramp smooth? Any walls or plateaus?
   - **Gate knobs**: Are progression thresholds fair and motivating?

4. Check for common problems:
   - Linear difficulty (should usually be exponential or S-curve)
   - Flat reward curve (diminishing returns keep things interesting)
   - Single dominant strategy (multiple viable approaches = better)

5. Present findings:
   ```
   BALANCED: [what's working]
   CONCERN: [what might be off, with specific numbers]
   SUGGESTION: [proposed change with reasoning from framework]
   ```

6. Write findings to learnings:
   ```bash
   pajama learning create -c balance -t "Balance check [date]" --content "[findings]"
   ```
