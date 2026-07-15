# 🎯 ReadTank

A lightweight **3D browser tank-battle game that helps kids learn to read.**

Bosses are unbeatable on the first attempt — when your tank is destroyed you
earn a **second chance only by reading a short passage and answering two
questions about it correctly.** Reading is the way forward, wrapped in a fun
arcade tank game.

Built with **React 19 + TypeScript + Vite + Tailwind + Three.js**. All 3D art
(tanks, arena, and the cartoony grass/rock textures) is generated
procedurally from primitives and canvas — **no external assets, no downloads,
no licensing**, and the Three.js bundle is the only heavy dependency.

## Gameplay

- **30 checkpoints.** Between each you fight **10 normal battles** against enemy
  tanks that grow stronger at every checkpoint (never mid-checkpoint) and keep
  one skin per checkpoint.
- **Checkpoint bosses** are guarded by normal tanks you must clear first. The
  boss is **invulnerable** at first and will destroy you — then you must read a
  passage and answer **2 multiple-choice questions** correctly to revive against
  a weakened-but-hard, defeatable boss. Wrong answers rotate in a fresh passage,
  so the only way through is to actually read.
- **Reading difficulty scales 1 → 5** across the campaign.
- **Unlock tanks:** you start with the *Cadet*; defeating each boss unlocks that
  boss's tank for later battles (31 tanks total).
- **Coins:** 1 coin per 5 tanks destroyed, 10 coins per boss.
- **Per-tank armoury (no universal upgrades):** every tank has its own permanent
  upgrades (hull, treads, auto-loader, heavy shells, extra barrels) and
  consumable power weapons (cluster bomb, airstrike), priced to be affordable
  for the point in the campaign where the tank is unlocked.

## Controls

- **Move:** `W A S D` / arrow keys (or the on-screen joystick on touch devices)
- **Aim:** mouse
- **Fire:** hold left mouse button or `Space` (or the on-screen FIRE button)
- **Power weapons:** `1` / `2` (or the on-screen buttons)

## Develop

```bash
npm install
npm run dev        # start the dev server (http://localhost:5173)
npm run test       # unit tests (progression, economy, content integrity)
npm run lint       # oxlint
npm run build      # typecheck + production build
```

### Browser smoke test

Drives the real WebGL game end to end, including the boss → reading → revive
loop (uses software WebGL so it runs headless):

```bash
npm run dev &                 # in one shell
node tank-e2e-smoke.mjs       # in another
```

## Project layout

```
src/tank/
  progression.ts   campaign maths: checkpoints, enemy/boss scaling, coins
  tanks.ts         the 31-tank roster
  addons.ts        per-tank upgrade + power-weapon catalogues
  passages.ts      the reading library (30 leveled passages, 2 MCQs each)
  loadout.ts       base stats + purchased upgrades -> effective stats
  store.ts         zustand + localStorage campaign save
  engine/          Three.js: game loop, procedural meshes, cartoony textures
  components/       React screens: menu, garage, shop, battle, reading, HUD
```

## License

[GNU AGPL v3](./LICENSE).
