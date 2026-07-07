# POTIONS

**[Play it →](https://fairley46.github.io/potions/)**

---

A 2D pixel sidescroller in two acts. One sitting. No save point — it doesn't need one.

## What it is

**Act I — The Way Out (~5 min)**
You're a hero on an adventure. Potions make you faster, stronger, able to break through walls and light up the dark. The world is vivid. The music drives forward. Monsters block your path and they drop exactly what you need when you fight them. You teach yourself to reach for the bottle.

**The Turn**
Seven lines of text. Then you face left.

**Act II — The Way Back (~5 min, feels longer)**
Same map, reversed. Half speed. No attack button — nothing left to fight. The elixir meter is gone. The music plays backward at 60 BPM. The monsters you killed are standing where you left them, and now you can see their faces.

Near home, one potion sits in the path. It's the only choice in the whole act.

## Design rules

The game never names what it's about. Not once. The player assembles the meaning — that's why it detonates.

Every mechanic doubles as metaphor, or it gets cut:
- Walls only break while buzzed. The level manufactures the need.
- Enemies drop potions. The violence feeds the need feeds the violence.
- The woods go dark unless you're drinking. You learn to stay lit.
- Tolerance rises. Drinking now just gets you back to normal.
- You can't die on the way back. You survive that part. That's the point.

## Shape

| | Act I | Act II |
|---|---|---|
| Direction | East → | ← West |
| Speed | Fast, escalating | Half speed |
| Color | Saturated, bright | Desaturated, gray |
| Music | Forward / 146 BPM | Reversed / 60 BPM |
| Combat | Yes | No |
| The choice | Automatic | One, deliberate |

Six named figures. Four zone mechanics. Zero bosses except yourself.

## Current state

`v0.4 prototype` — playtest phase.

The one metric: **do players describe the feeling of the turn unprompted?** If they lead with controls or combat, something isn't working. If they go quiet first, it's working.

Known rough edges:
- Figures are chunky rect-humanoids (pixel-sprite pass is the biggest visual win available)
- Potion pickup hitbox is slightly tight on high-floating bottles
- Playtest tuning is still first-pass — the numbers are guesses until they're not

## Play

Open `potions.html` in any browser, or use the link above. No build, no install, one file.

**Controls:** Arrow keys / WASD · Space to jump · J to attack · M to mute · Enter to start

Sound on. One melody. Two lives.

## Files

| File | Purpose |
|---|---|
| `potions.html` | The game — single self-contained file, no deps |
| `POTIONS-beat-map.md` | Full design spec: zones, mechanics, iteration protocol |
| `CLAUDE.md` | Brief for Claude Code — architecture, tuning knobs, working model |
