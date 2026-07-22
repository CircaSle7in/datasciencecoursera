# ROSEDOKU // HeatherOS 🌹

A cozy, **ad-free** garden logic puzzle — a Queens-style deduction game (think
LinkedIn Queens crossed with Minesweeper), reimagined as **planting roses**, and
skinned to match the **heatherblood.com** brand: deep-purple neo-brutalism,
hot-pink/yellow/cyan/lime color-blocks, hard black offset shadows, heavy display
type over monospace, caution tape, a green terminal readout, and a **compliment
generator**.

One self-contained HTML file: no install, no network, no tracking. Just roses.

_(Originally a cat-themed "Meowdoku" clone — see git history. The folder keeps
the `meowdoku/` name.)_

## Play

Open `meowdoku/index.html` in any browser (phone, tablet, or laptop).
**On a phone:** open it and tap the browser's *"Add to Home Screen"* — it
launches full-screen like a real app.

## The rules

Each garden is split into colored **beds**. Plant roses so that:

- **one rose in every row**, **every column**, and **every colored bed**,
- and **no two roses ever touch** — not side by side, not even at a corner
  (diagonally).

Every garden has exactly **one** solution, always reachable by pure logic.

## How to play

- **Tap a tile** to cycle: empty → **✕** (bare dirt, ruled out) → **🌹** (rose) →
  empty. Use ✕ like Minesweeper flags to mark spots you've eliminated.
- **Plant in the wrong spot and a 🪲 Japanese beetle moves in.** Three beetles
  and the garden's overrun — replant it or start fresh.
- Hit **NEED A COMPLIMENT?** anytime for a pick-me-up. 🌹

## Features

- **9 levels** that grow from **6×6 (Windowbox)** to **14×14 (Rose Witch)**,
  with a scrollable ladder, per-level best times, and "Next level" progression.
- **Garden Almanac** — persistent stats: gardens bloomed, win rate, current &
  best streak, roses planted, beetles suffered, and per-level records.
- **Undo**, **Clear**, **Hint**, and a **compliment generator** in Heather's voice.
- **Easter eggs** hidden throughout (🥚 6 to find). Keep your eyes open.
- Guaranteed unique, logic-solvable gardens, generated fresh in a background
  worker so even the big boards never freeze.
- **Auto-saves**, works fully offline.

### About the generator (the math)

Each garden must have exactly one solution. The generator:

1. builds a random valid rose layout (one per row/column, none touching),
2. floods random colored beds outward from each rose,
3. **carves for uniqueness** — repeatedly finds alternate solutions and nudges a
   boundary cell into a neighbor bed to kill them (never touching a rose cell, so
   the intended solution always survives),
4. **bails and regrows** if a garden won't converge in ~40 passes.

The uniqueness solver uses **unit propagation + MRV** (minimum-remaining-values)
branching with a node budget — which also guarantees every garden is solvable by
pure logic. This scales generation cleanly to 14×14 (median ~100ms, worst <1s),
up from a 9×9 ceiling.

**Puzzle bank:** the higher levels (10×10–14×14) also ship a bank of ~90
pre-generated, uniqueness-verified gardens (compactly hex-encoded, ~15KB). Those
levels are served instantly from the bank and recycled, so the big boards never
wait on generation and stay reliable even where a background worker isn't
available. Smaller levels (6×6–9×9) are generated fresh every time.

Made with love for the Rose Witch. 🌹🐝
