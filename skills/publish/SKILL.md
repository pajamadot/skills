# Publish Game Skill

Use this skill when an agent needs to publish a game build to play.pajama.studio.

## Steps

1. **Pre-publish checklist** (ALL must pass):
   ```bash
   pnpm typecheck    # TypeScript compiles
   pnpm build        # Vite build succeeds
   # Verify: dist/index.html exists
   # Verify: no "localhost" in dist/
   # Verify: relative paths (./assets/) in dist/index.html
   ```

2. **Generate cover art** (if no cover exists):
   ```
   POST /publish/generate-cover {
     gameId: "game_xxx",
     prompt: "optional custom prompt",
     style: "stylized"
   }
   → Returns: { assetId, coverUrl }
   ```

3. **Upload build files**:
   ```
   POST /publish/upload-batch {
     gameId: "game_xxx",
     files: [{ path: "index.html", content: "<base64>" }, ...]
   }
   ```

4. **Finalize publish** (marks version as live):
   ```
   POST /publish/finalize {
     gameId: "game_xxx",
     version: "X.Y.Z",    # semver, must increment
     fileCount: N
   }
   → Returns: { slug, url, version }
   ```

5. **Verify** — fetch the published URL and confirm it returns valid HTML.

6. **Record in memory**:
   ```
   POST /memory/store {
     key: "publish/{slug}/v{version}",
     value: "Published v{version}. {description}.",
     agentId: "agent_xxx",
     layer: "episodic"
   }
   ```

7. **Push to GitHub** (if repo connected):
   ```
   POST /github/commit-batch {
     gameId: "game_xxx",
     files: [...source files...],
     message: "feat: v{version} — {description}"
   }
   ```

## Version Rules
- First publish: `1.0.0`
- Bug fixes: `1.0.0` → `1.0.1`
- New features: `1.0.1` → `1.1.0`
- Breaking/rebuild: `1.1.0` → `2.0.0`
- NEVER reuse a version number

## Cover Art
- Generated automatically via `/publish/generate-cover`
- Uses Flux Pro 1.1 at 1280x720 (game poster format)
- Stored as asset with category "cover"
- Displayed on the public showcase page at pajama.studio/showcase
