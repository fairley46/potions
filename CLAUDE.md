# POTIONS — project brief for Claude Code

## What this is

A five-minute 2D pixel sidescroller about addiction, told entirely through mechanics. The word "addiction" (or "alcohol," or "sober") never appears in the game — that's rule #1. The player gets hooked on potions during a power-fantasy beat-em-up run east ("the way there"), then walks home west through the wreckage in withdrawal ("the way back"). The turn — realizing the monsters were people who loved you and the adventure was your real life — is the entire payload. Everything serves that firework.

Currently v0.4: a single self-contained file, `potions.html`. No build step, no dependencies, no framework. Keep it that way unless Brad explicitly says otherwise — the simplicity is the elegance.

## Design laws (non-negotiable, in priority order)

1. **The game never names its subject.** No "addiction," "alcohol," "sober," "relapse" in any player-facing text. The player assembles the meaning; that's why it detonates.
2. **Every mechanic must double as metaphor, or it's cut.** Examples in place: tolerance ticks raise elixir drain (dependency escalates); walls only break buzzed and woods only light up buzzed (the level manufactures the need); enemies drop potions (the violence feeds the need feeds the violence); no attack button in Act II (nothing left to fight); you can't die on the way back (you survive that part — that's the point).
3. **Add investment, not length.** Target stays ~5 minutes each way. If a change doesn't deepen the player's relationship with potions or with a loved one, it's padding.
4. **The way back is sacred.** Slow, gray, quiet, unwinnable, uninterruptible. Don't add challenge, collectibles, or pacing "improvements" to Act II. Its emptiness is the content.

## Architecture (all in potions.html, one <script>)

- Internal canvas 320×180 (`buf`/`bctx`), integer-upscaled to screen (`screen`/`sctx`), imageSmoothing off.
- **Text renders on a separate hi-res overlay**: queue via `T(str,x,y,size,col,align,alpha,bold)`, flushed by `flushText()` after the buffer blit. Never draw text into the low-res buffer.
- State machine: `title → act1 → turn → act2 → end`, driven in `frame()`.
- Global saturation `SAT` (0–1.2) desaturates every color drawn through `C(h,s,l)`. The buzz raises it, withdrawal and Act II crush it. All world colors must go through `C()`.
- Key systems: `updateAct1` (movement, potion economy, wall/darkness gates, mob spawner, combat), `updateAct2` (the walk home, loved-one reveals, the single Act II potion), `drawLandmarks` (same buildings, fantasy-skinned in Act I, real in Act II), `player.kills[]` (positions of everyone killed; they stand there in Act II).
- Audio: WebAudio, no assets. `MEL` is one 16-step melody — played forward/square/146bpm in Act I, **reversed**/triangle/60bpm in Act II. Withdrawal detunes everything to 0.94. SFX via `sfx(kind)`. Audio inits on first keydown (browser autoplay policy).
- Named characters live in `LOVED` (Mom must remain the last figure before home). Generic crowd labels in `CROWD`.

## Tuning knobs (where the feel lives)

- Elixir drain: `3.2 + tol*1.35` in updateAct1 — the dependency curve.
- Power scaling: `power = min(potionsDrunk,16)` → speed `78+power*4`, damage `1+(power/3|0)`, jump, knockback, shake.
- Spawner: interval `max(0.7, 3.0 - x/1100 - power*0.09)`, cap 7 alive, 50% potion drop.
- Act II walk speed 40 (25 wounded-facing-right). Resist the urge to speed it up.

## Current state / known rough edges

- Figures are chunky rect-humanoids; a real pixel-sprite pass (2-frame walk, hurt flash) is the biggest visual win available.
- Potion pickup hitbox is slightly tight for the highest-floating bottles.
- Enemy knockback can shove the player through the parallax edge cases near walls (cosmetic).
- Playtest tuning is unfinished — the numbers above are first guesses.

## The iteration protocol (how we know it's a gem)

The one metric: playtesters describe **the feeling of the turn** unprompted. If they talk about controls or combat first, fix investment, not features. Cut order when something drags: combat depth first, zone length second, loved ones never.

## Working with Brad

Brad is the designer; treat the emotional beats as spec, not suggestion. He values restraint — when in doubt, do less, and flag ideas as options rather than shipping them. Small, playable iterations beat big refactors. Before any structural change, ask: does this make the turn hit harder?

## Repo housekeeping

Files: `potions.html` (the game), `README.md`, `POTIONS-beat-map.md` (design doc), this file. Sensible first commits: init repo, then one commit per playable change with messages describing the *felt* change ("act II walk feels longer", not "adjusted constant").
