# 🌲 FOREST RUN

A cartoon‑forest **battle royale** that runs entirely in the browser. 50 players drop into a scrolling forest map, a storm slowly closes in, and the last one standing wins. Pick from **20 classes**, climb a **10‑level boss ladder**, unlock characters through achievements, and level up a battle pass — all packed into a single HTML file with **no build step and no dependencies to install**.

> Open `index.html` in any modern browser and play. That's it.

---

## ✨ Highlights

- **Battle royale for 50** — a shrinking storm forces everyone toward the center; survive the longest to win.
- **A big 7×7 world** — 49 "pages" you walk between by stepping off the edge of the screen. Structures to duck into, loot to grab, and trees/bushes that hide you from enemies.
- **20 playable classes**, each with a unique 3‑ability kit (Q / E / R) plus a basic attack.
- **10‑level boss ladder** — hand‑drawn bosses, each with its own look, stats, and mechanics. Beat one to unlock its class.
- **Achievements & unlocks** — most classes are earned by doing something specific (win a match, win without taking damage, reach the top 3 without a kill, defeat a boss, …).
- **Battle pass** — earn XP every match for better placements; level up to unlock cosmetics and classes.
- **Party system** — group up with friends and drop into a match together.
- **Full mobile support** — a virtual joystick and a reorganized touch HUD, so it plays well on a phone.
- **Optional online multiplayer** — real players can share a match; if the network layer can't load, it seamlessly falls back to single‑player.

---

## 🎮 Controls

| Action | Keyboard | Touch |
|---|---|---|
| Move | `W` `A` `S` `D` / arrow keys | Virtual joystick (bottom‑left) |
| Basic attack | `Space` | Attack button |
| Ability 1 / 2 / 3 | `Q` / `E` / `R` | Ability pad (bottom‑right) |

Walk to the **edge of the screen** to cross into the neighboring page of the map. Watch the minimap and the storm timer — get caught outside the safe zone and you take damage over time.

---

## 🧙 Classes

**Starter / core classes** include Wizard, Tank, Glass Cannon, Ranger, Cryomancer, Blademaster, Engineer, and Paladin — a spread of ranged casters, bruisers, glass‑cannon burst, mobility, crowd control, and support.

**Unlockable classes** are earned rather than picked from the start. A few examples:

- **Blademaster** — win your first match.
- **Cryomancer** — get frozen by one.
- **Glass Cannon** — win a match without taking any damage.
- **Civilian** — a no‑attack survivor built around escape and misdirection (Escape Portal, Vanish, Decoy). Earned by reaching the **top 3 without a single kill**.
- **9 boss classes** (Ghoul, Wraith, Rot Knight, Plague Doctor, Revenant, Bonelord, Necromancer, Lich, The Undying) — unlocked by clearing the matching level of the boss ladder.

When you unlock a class, a banner slides in announcing it, and the class appears in the picker for future matches.

---

## 💀 Boss Ladder

A separate **Boss Fight** mode is a 1‑vs‑1 escalation against 10 increasingly dangerous bosses, shown left‑to‑right and beaten in order:

1. Zombie → 2. Ghoul → 3. Wraith → 4. Rot King → 5. Plague → 6. Revenant → 7. Bonelord → 8. Necromancer → 9. Lich → 10. The Undying

Each boss is drawn from scratch on the canvas (no sprite images), gets tougher in HP, damage, speed, and cast rate, and uses its **own set of mechanics** — lunges, whirls, homing projectiles, telegraphed strikes, pulls, walls, auras, and more. Clearing a level permanently unlocks that boss's class and its achievement.

---

## 🕹️ How progression works

- **XP & Battle Pass** — every match awards XP based on placement (and a bonus for winning). XP levels up your battle pass, which gates some classes and cosmetics.
- **Achievements** — persistent per‑account (or per‑browser as a guest). Many double as class unlocks.
- **Accounts** — optional local accounts keep your level, achievements, unlocked classes, and avatar. Guests keep progress in the browser and can convert to an account later.

All progression is stored locally in the browser (via `localStorage`) — there is no account server.

---

## 🌐 Multiplayer

Online play is powered by [PlayroomKit](https://joinplayroom.com/), loaded at runtime from a CDN. When it's available and you're online, real players can share a session; positions, the bot roster, and the storm are synchronized between everyone in the same room. The **party system** is the reliable way to play with friends.

If the network layer can't load (offline, blocked, or on a static host with a strict content policy), the game **catches the error and runs as a polished single‑player experience** instead — quick match against 50 bots still works exactly the same.

---

## 🛠️ Tech & architecture

- **One self‑contained file.** `index.html` holds the markup, all CSS (in a `<style>` block), and all game logic (in `<script>` blocks). No frameworks, no bundler, no `node_modules`.
- **Canvas 2D rendering** for the world, characters, storm, and all hand‑drawn bosses and effects.
- **`requestAnimationFrame` game loop** with a fixed max delta, so the simulation stays stable across frame rates.
- **Page‑bucketed AI** — bots are grouped by map page each frame for efficient targeting, so all 50 stay active across the whole map rather than only near the player.
- **Responsive layout** — the HUD reorganizes into non‑overlapping zones on phones, and the world rescales cleanly when the window is resized mid‑match.
- **The only external dependency is the optional multiplayer CDN import**, which is failure‑tolerant by design.

---

## 🚀 Running it

**Just open the file:**

```
index.html
```

Double‑click it, or drag it into a browser tab.

**Or serve it locally** (recommended if you want the multiplayer layer to load reliably):

```bash
# Python 3
python -m http.server 8791
# then visit http://localhost:8791/index.html
```

Any static file server works — the project is a single static asset.

---

## 📁 Project structure

```
.
├── index.html   # the entire game — HTML, CSS, and JS in one file
└── README.md    # this file
```

That's the whole project. Everything — rendering, 20 classes, bots, the storm, the boss ladder, achievements, the battle pass, mobile controls, and the optional multiplayer bridge — lives in `index.html`.
