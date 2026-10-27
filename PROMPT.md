# Prompt

Isti prompt dobila su oba modela. Lokalni model je u 2. i 3. krugu uz njega dobio i svoj dotadašnji kod te opis grešaka koje smo vidjeli u igri.

## System

You are an expert game programmer. You write complete, working, self-contained code. When asked for a file, you answer with the complete file in one ```html code block and nothing after it.

## User

Write a complete 2D pinball game that runs in a desktop web browser, in the style of the retro video pinball game "Pinball Deluxe: Reloaded": a single tall portrait table, viewed straight from above, with bright illustrated artwork, metallic parts, and a dot-matrix score display.

**Delivery**
- One file `index.html` with all HTML, CSS and JavaScript inline. No libraries, no frameworks, no build step, no network requests. It must work when opened directly from disk (file://).
- Optional images: `assets/playfield.jpg` (1024x2048, artwork under the playfield) and `assets/wall.jpg` (background around the table). Load them with `<img>`/`Image()`. If an image fails to load, draw a fallback (dark blue gradient for the playfield, dark grey for the wall). The game must be fully playable without them.
- Draw everything with the Canvas 2D API. All physical parts (walls, rails, bumpers, targets, flippers, plunger, ball) are drawn by code on top of the playfield image, never baked into it.

**Screen layout**
- Logical table size 600 x 1200 units. Scale it to fit the window height, keep the aspect ratio, centre it. The rest of the window shows `wall.jpg`. Handle window resize.
- A dot-matrix display (amber dots on dark red-brown, like a real DMD) at the top right outside the table, showing `BALL n` and the score with thousands separators. It also shows short messages for 1.5 s ("ORBIT 2,500", "BONUS 4X", "MULTIBALL!", "BALL SAVED", "GAME OVER").

**Table elements** (place them like a classic table, use your judgement for exact positions)
- Outer wall with a rounded top arch.
- Plunger lane on the right side, with a spring plunger at the bottom and a one-way gate at the top of the lane, so the ball cannot fall back into the lane.
- Two flippers at the bottom with a drain gap between them. Two slingshots (triangular kickers) above the flippers, with inlanes and outlanes on both sides.
- Three pop bumpers in the upper middle area.
- Three rollover lanes at the very top (lights L1, L2, L3).
- A bank of 4 drop targets on the left side.
- A kickout saucer (hole that catches the ball and ejects it after 1 s) on the right side.
- An orbit: a lane that runs from the left side, around the top arch, and comes back down on the right.
- Five bonus multiplier lights (1x 2x 3x 4x 5x) drawn as stars above the flippers, as in the reference game.
- Insert lights for all lit features (lanes, targets, saucer, multipliers) that glow when lit.

**Physics** (this matters most; it must feel like a real pinball)
- Fixed timestep of 1/120 s with at least 8 substeps per step, so a fast ball never passes through a wall or a flipper.
- Gravity along the table is 1,200 units/s². Ball radius 10 units. Limit the ball speed to 2,500 units/s.
- Circle collisions against line segments, arcs and circles, with restitution and some friction. Walls restitution 0.5, rubber posts and slingshots 0.8.
- Flippers are rotating capsules (length 80, rounded ends). They swing up at about 1,500°/s. The flipper's surface velocity at the contact point must be added to the ball's bounce, so the ball can be shot hard up the table and cradled on a held flipper.
- Pop bumpers and slingshots actively kick the ball away (bumper about 900 units/s). Animate the kick.
- Plunger: hold to pull back (up to 1 s), release to shoot. Launch speed proportional to the hold time; full power must reach the top of the table.

**Controls**
- Left flipper: Left Shift, Z or Left Arrow. Right flipper: Right Shift, / or Right Arrow.
- Plunger: Space or Down Arrow (hold and release).
- Start a new game: Enter. Pause: P.
- While a flipper key is pressed, the lit top rollover lanes rotate left or right (lane change, like on a real table).

**Rules**
- 3 balls per game. Ball save: for the first 10 s of each ball, a drained ball is returned to the plunger with "BALL SAVED".
- Scores: pop bumper 100, slingshot 10, rollover lane 500, drop target 1,000, saucer 5,000, orbit 2,500 (a second orbit within 3 s scores double).
- All three top lanes lit: bonus multiplier +1 (max 5x), the lanes reset.
- All four drop targets down: they reset after 2 s and the saucer lights for a jackpot of 25,000.
- Three saucer jackpots in one ball: 2-ball multiball, with a second ball launched from the plunger. Multiball ends when one ball is left.
- End-of-ball bonus: (number of targets, lanes and bumpers hit this ball) x 100 x bonus multiplier, counted up on the display.
- After the last ball: "GAME OVER". Save the high score in localStorage inside try/catch, so the game still works if storage is blocked.

**Sound**
- Short synthesized sounds with the Web Audio API (flipper, bumper, target, drain, jackpot). Create the audio context on the first key press. No audio files.

**Code quality**
- Readable code with clear sections (setup, table geometry, physics, rules, rendering, input). No errors in the browser console.

Answer with the complete index.html file only.

