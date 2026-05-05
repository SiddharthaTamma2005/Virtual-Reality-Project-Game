# 🐜 ANT Colony: Descent

A browser-based first-person shooter set inside a giant ant colony. Fight your way through organic underground tunnels, collect weapons and food, and destroy the Ant Queen in her chamber deep below the surface.

---

## Overview

**Ant Colony: Descent** is a self-contained, single-file HTML5 game built with [Three.js](https://threejs.org/). No installation or build step is required — just open `index2.html` in a modern browser and play. The game also supports **WebXR** for VR headset play.

---

## How to Play

Open `index2.html` in a browser (Chrome or Firefox recommended). Click the canvas to lock the mouse pointer, then use the controls below.

### Controls

| Action         | Input                        |
|----------------|------------------------------|
| Move           | `W` `A` `S` `D`              |
| Look           | Mouse                        |
| Jump           | `Space`                      |
| Attack         | Left Click                   |
| Pick up item   | `E`                          |
| Eat food       | `F`                          |
| Switch weapon  | `1` – `5` (hotbar slots)     |
| Enter VR       | Click the **◈ ENTER VR** button (requires compatible headset) |

### VR Controls (WebXR)

When playing in VR, weapons and movement are adapted for the headset. A grip button is used in place of `E` to pick up items. The hotbar and HUD are hidden; a simplified 3D UI is shown instead.

---

## Objective

Descend through the winding ant colony tunnel from the surface down to the **Queen's Chamber** at the bottom. Kill the Ant Queen (300 HP) to win. If your health reaches zero, you die and must refresh to restart.

---

## Gameplay Systems

### Health
- You start with **100 HP**.
- Ants deal **6 damage** per hit. The Queen deals **15 damage** per hit.
- The HP bar in the top-right changes color as health drops (green → yellow → red).
- A red flash overlay appears on screen when you take damage.

### Weapons
Weapons are found as glowing pickup orbs scattered along the tunnel path. Press `E` to pick up a weapon; it fills into the next empty hotbar slot (or replaces your active slot if full).

| Slot | Weapon          | Damage | Range | Ammo    | Description          |
|------|-----------------|--------|-------|---------|----------------------|
| 1    | Magnifying Glass| 18     | 4     | ∞       | Focused heat beam    |
| 2    | Bug Spray       | 9      | 7     | 35      | Chemical aerosol     |
| 3    | Steel Boot      | 32     | 2     | ∞       | Maximum stomping     |
| 4    | Flamethrower    | 14     | 5     | 25      | Incendiary burst     |
| 5    | Tweezers        | 48     | 2     | ∞       | Surgical precision   |
| —    | Ant Acid        | 22     | 5     | 18      | Corrosive spray      |

Each weapon has a unique 3D hand model visible in the bottom-right of the screen, with a muzzle flash effect when fired.

### Food
Green glowing orbs are food pickups. Press `E` to collect food into the dedicated **F-slot** in the hotbar, then press `F` to eat it and restore HP.

| Food       | HP Restored |
|------------|-------------|
| Crumb 🍞   | 20          |
| Berry 🫐   | 35          |
| Mushroom 🍄| 50          |
| Honey Drop 🍯| 70        |

Food stacks if you pick up the same type twice.

### Enemies
- **Worker Ants** — Patrol the tunnel and chase you when within range. They have 15 HP each and respawn if the count drops below 6.
- **Queen Ant** — Located at the deepest point of the colony (Z = -62). She has 300 HP, moves faster than workers, and hits harder (15 damage per attack). A health bar floats above her.

### Kill Feed & Depth Tracker
- The **KILLS** counter and **DEPTH** label in the top-left update in real time.
- Depth is reported as `SURFACE`, `SHALLOW`, `MID`, `DEEP`, or `QUEEN'S CHAMBER` based on your Z position in the tunnel.

---

## World

The level is a single procedurally styled organic tunnel following a curved Catmull-Rom spline from the surface (Z ≈ +10) down to the Queen's Chamber (Z ≈ -62), with four branching side tunnels. The tunnel geometry uses vertex colors and normal displacement to simulate rough, dirt-packed walls.

**Atmospheric details include:**
- Bioluminescent mushrooms with point lights
- Hanging root strands
- Ant egg clusters near the Queen
- Dust particle system
- Exponential fog that thickens with depth
- Animated breathing vignette and CRT scanline overlays

---

## Technical Details

- **Renderer:** Three.js r128 (`WebGLRenderer`), loaded from CDN
- **No build system:** Single HTML file, no npm, no bundler
- **VR:** WebXR support via `renderer.xr.enabled = true`; enter with the in-game button
- **Performance:** Shadow maps disabled; instanced mesh used for all worker ants; pixel ratio capped at 1.5×
- **Compatibility:** Requires a browser with WebGL 2 support (Chrome 80+, Firefox 75+, Edge 80+)

---

## File Structure

```
index2.html   ← entire game (HTML + CSS + JavaScript, ~1,500 lines)
README.md     ← this file
```

---

## Restarting

There is no in-game restart button. Refresh the page (`F5` / `Ctrl+R`) to start a new run.
