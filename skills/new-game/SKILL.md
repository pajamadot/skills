# /new-game — Create a New Game Project

Scaffold a new game project from a template.

## Process

1. Ask: What engine?
   - `phaser-2d` — Phaser 3 (2D arcade, pixel art, platformers, runners)
   - `three-3d` — Three.js (3D first/third person, open world, WebGL)
   - `playcanvas` — PlayCanvas (3D ECS, mobile-first, WebGPU-ready)

2. Ask: Game name? (kebab-case: `my-cool-game`)

3. Scaffold:
   ```bash
   cp -r templates/{engine}/ games/{name}/
   cd games/{name}
   pnpm install
   ```

4. Register with API:
   ```bash
   curl -X POST https://api.pajama.studio/api/v1/games/create \
     -H "Content-Type: application/json" \
     -d '{"name":"[Name]","engine":"[engine]","repoPath":"games/[name]"}'
   ```

5. Guide to next steps:
   - "Write a GDD: use `/design-system`"
   - "Or brainstorm ideas: use `/brainstorm`"
   - "Quick prototype: just start coding in `src/`"

## Available Templates

| Template | Engine | Best For |
|----------|--------|----------|
| `phaser-2d` | Phaser 3 | 2D games: platformers, runners, puzzles, top-down |
| `three-3d` | Three.js | 3D games: exploration, walking sims, FPS prototypes |
| `playcanvas` | PlayCanvas | 3D games: mobile-ready, physics-heavy, ECS architecture |
