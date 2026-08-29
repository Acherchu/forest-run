# FOREST RUN

Cartoon-forest **battle royale** that runs entirely in the browser. 50 players, a closing
storm, 20 classes, a 10-level boss ladder, battle pass, party system, mobile touch controls,
and optional online multiplayer.

## The one rule

**Everything lives in `index.html`.** ~5150 lines, no build step, no dependencies, no
package.json. Open the file and it runs. Do not add a bundler, npm install, or split it into
modules — self-contained is the design, not an accident.

## Run it

```bash
start "" "C:\Users\arche\play-button-game\index.html"
```

Or serve it (needed if testing anything that requires a real origin rather than `file://`):

```bash
"C:\Python314\python.exe" -m http.server 8080 --directory "C:\Users\arche\play-button-game"
```

Then open `http://localhost:8080`. A `.claude/launch.json` is set up, so `preview_start`
with name `forest-run` also works.

## File layout inside `index.html`

| Lines | What |
|---|---|
| 4–880 | `<style>` — all CSS |
| 1394–5144 | main `<script>` — the entire game |
| 5147–5152 | `<script type="module">` — multiplayer bootstrap |

Navigate the main script by its banner comments (`// ---------- name ----------`):

- **1416** sound effects (Web Audio, synthesized — no audio files anywhere)
- **1461** profile persistence · **1479** profanity filter
- **1568** flow: menu → matchmaking · **1633** battle · **1911** lobby fill to 50
- **1788** achievements (persisted per-browser via localStorage)
- **2014** Zombie Boss fight · **2038** party system
- **2144** page-by-page adventure (the 7×7 world)
- **2368** touch controls / virtual joystick
- **2386** multiplayer (PlayroomKit, hosted + authoritative)
- **2598–3228** ability system: boss primitives, 30 boss abilities, melee, anime-style
  abilities, Zombie class, boss-class abilities, bot kits
- **3541** spectate-after-death · **3724** battle royale storm + bots

## Conventions

- Art is **hand-drawn in canvas code**, not sprites/images. New visuals get drawn the same
  way — match the surrounding drawing style (see git log: several commits are pure art
  redraws to keep abilities visually consistent).
- Multiplayer is authoritative for damage (`phit`/`hit`); visuals are broadcast separately so
  everyone sees projectiles. Keep that split — don't make damage client-side.
- If the network layer fails to load, the game must still fall back cleanly to single-player.

## Git

Remote `origin` → https://github.com/Acherchu/forest-run, branch `main`. This is the only
game here with a remote. After a meaningful change, offer to commit and push — ask first.
