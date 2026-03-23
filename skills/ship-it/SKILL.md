# /ship-it — Build, Deploy, and Release

Build and deploy a game to production.

## Pre-Release Checklist

1. All critical tasks completed? `curl $API/tasks/available` — none at P8+
2. No open bugs at P7+?
3. Game runs without crashes?
4. Performance acceptable (60fps target)?

## Build & Deploy

```bash
GAME="pajama-runner"  # or the game being shipped

# Build
cd games/$GAME
pnpm build

# Deploy to Cloudflare Pages
npx wrangler pages deploy dist --project-name $GAME --branch main

# Verify
curl -s -o /dev/null -w "%{http_code}" https://$GAME.pages.dev/
```

## Post-Deploy

1. Update game status: `curl -X PUT $API/games/GAME_ID/status -d '{"status":"shipped"}'`
2. Broadcast: `pajama message broadcast -s "Game shipped!" -b "$GAME deployed to production"`
3. Write memory: `pajama memory write "release/$GAME-v1" "Shipped on [date]. Build: [commit]. URL: [url]"`
4. Create follow-up tasks for post-launch monitoring
