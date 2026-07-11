# POTIONS — Beat Map
*Target: ~5 minutes each way. Short like Passage — every element carries weight or gets cut.*

> **Note:** this doc holds both the original zone plan (below) and the implemented-state changelog (bottom). The prototype compressed the 4-zone plan into one continuous 5-minute run — the zone *powers* survived as the wall/darkness gates.

## Design law (the anti-overdoing rules)
1. The game never says "addiction," "alcohol," or "sober." Not once. The player assembles the meaning — that's why it detonates.
2. Every mechanic must double as metaphor, or it's cut.
3. No text moment longer than 7 lines.
4. Add investment, not length. If a section doesn't deepen the player's relationship with potions or a loved one, it's padding.

---

## ACT I — THE WAY OUT (~25 min)
Each zone does exactly two jobs: introduce one loved one (as a monster), and one potion power **the level quietly requires**. The player teaches themselves to reach for the bottle.

### Zone 1 — The Front Yard
- **Feel:** golden hour, warm, easy. Almost a celebration.
- **Potion power:** none needed — the first potion is a pure *choice*. Sits on a table like a toast. Optional. Feels great: speed, glow, music swells.
- **Monster:** MOM (shadow). Easy fight. She "blocks the gate."
- **Lesson taught:** potions = joy. No cost visible.

### Zone 2 — Town
- **Potion power:** STRENGTH — cracked walls only break while buzzed. First *mandatory* potion.
- **Monster:** GRANDMA (shadow), standing in a doorway.
- **Escalation:** elixir drain becomes noticeable. First "You need another one."
- **Detail for the way back:** every wall you break stays broken.

### Zone 3 — The Dark Woods
- **Potion power:** GLOW — the screen dims to near-black unless buzzed. Potions light the way.
- **Monsters:** DANNY (your brother) and THE DOG (small, doesn't fight back — the player has to choose to get past it).
- **Escalation:** potions spaced farther apart. Somewhere in here, the player skips a fight to grab a bottle. Don't force it — design the spacing so it *happens*. That moment is the whole game working.

### Zone 4 — The Ascent
- **Potion power:** LEAP — gaps only clearable buzzed.
- **Monster:** SARAH. Hardest fight so far.
- **Escalation:** tolerance so high the buzz barely brightens the screen anymore. Diminishing returns made *visible* — drinking now just gets you back to normal.
- **Final encounter, steps from the light:** YOU. Your own silhouette. Strongest enemy in the game.

### The Turn
The light is just a light. Seven lines, max. Then face left.

---

## ACT II — THE WAY BACK (~10 min real time; designed to feel longer)
Same map, reversed. Half speed. No attack button. No elixir meter — the UI itself has gone quiet.

- **Reverse order matters:** Sarah → the Dog → Danny → Grandma → **Mom last, steps from home.** Her line lands final.
- **You walk over your own damage:** the walls from Zone 2 are rubble underfoot. The woods stay dark — you walk through anyway, and it turns out you can. The gaps you leapt are climbed down, slowly.
- **The one choice in the whole act:** near home, a single potion sits on the path — the only one in Act II. Take it: three seconds of color and warmth, then it cuts out, and the end card changes ("day one" starts over). Walk past it: nothing happens. No fanfare, no reward. *That's the point.*
- **Home:** the warm window. The only saturated color left in the world.

### End card
- "You drank N potions on the way there."
- "You needed zero on the way back." *(or: "You needed one. Day one starts again." — if they took it)*
- Title reveal: **POTIONS**.

---

## How we know it's a gem (iteration protocol)
- **The one metric:** playtesters describe *the feeling of the turn* unprompted. If they talk about controls or combat first, the firework fizzled — fix investment, not features.
- **Cut order when something drags:** combat depth first, zone length second, loved ones never.
- **Prototype loop:** v0.2 = zone powers + mandatory-potion walls → test → v0.3 = the Act II choice + reverse encounters → test → v0.4 = art/sound pass (warm hum that detunes in withdrawal) → test → decide if it's real.

## Scope guard
One player character, six figures, four zone gimmicks, zero bosses except YOU, no inventory, no dialogue trees, no save system beyond the day counter (it's one sitting — like Passage, that's a feature).

---

# Changelog

## v0.7 — mercy has a memory
- Spare tracking: walk 90px past a family member without killing them → "It let you go. It watched you leave." They stop following.
- Every LOVED entry has paired lines: killed vs spared. Danny killed: "he called every Sunday, for a while" / spared: "he still calls every Sunday."
- True sober ending: zero potions → no enemies ever spawn, family visible as people from Act I, color blooms back at home, family gathered at the house.
- Act II temptation system: the path bottle (now jumpable — jump raised to clear it, barely), one that rolls out of the rubble you made, and a man outside the bar who offers you one if you linger. Beaten by not stopping.
- Resistance counted: "it found you 3 times on the way back. you kept walking."

## v0.6 — the sober route exists
- All potions grounded and jumpable; tight pickup boxes. "You walked past it." + passed counter.
- Walls break in 10 sober hits ("It barely gives. But it gives.") or 1 buzzed hit.
- Day counter persists across runs (localStorage, guarded). Taking the Act II potion resets to day one.
- Hidden sober payoff: no potions → no monsters, anywhere. There never were any.
- Copy fix: dark-woods hint no longer implies an inventory.

## v0.5 — the truest sentence
- Family never attacks in Act I — they hold on and slow you. Only strangers and YOU deal damage.
- Inner voice escalates from "Warmth." to "They keep getting in your way."
- Craving heartbeat (audio + vignette pulse) below 25 elixir. Act II reveal holds (you stop and face them).
- Shovel-Knight-adjacent art pass: outlined pixel sprites (same body for people and shadows — the reveal is literal), 12-band sky, clouds/fog, layered glows, euphoric aura, slash arcs, landing dust, jump/land sfx, sparkle echo + pad swell music layers.

## v0.4 — resolution, landmarks, sound
- Hi-res text overlay above the pixel buffer.
- Landmarks skinned twice: castle/spires/tower/glowing den on the way out → school/dorms/office/bar on the way back.
- WebAudio chiptune: one melody, forward 146bpm out, reversed 60bpm back; withdrawal detunes the world. Full SFX set.

## v0.3 — the buzzsaw
- Power stacks per potion (speed/damage/jump/knockback). Mob spawner scales with distance and habit. Enemies drop potions. Final surge. The crowd waits on the way back with labels.

## v0.2 — the 5-minute cut
- Walls and darkness gates, YOU as the final fight, the single Act II potion, "day one starts again."

## v0.1 — the loop
- Two acts, tolerance/elixir economy, palette desaturation, loved-one reveals, the walk home.
