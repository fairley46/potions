# POTIONS — project brief for Claude Code

## What this is

A five-minute 2D pixel sidescroller about addiction, told entirely through mechanics. The word "addiction" (or "alcohol," or "sober") never appears in the game — that's rule #1. The player gets hooked on potions during a power-fantasy beat-em-up run east ("the way there"), then walks home west through the wreckage in withdrawal ("the way back"). The turn — realizing the monsters were people who loved you and the adventure was your real life — is the entire payload. Everything serves that firework.

Currently v0.7: a single self-contained file, `potions.html`. No build step, no dependencies, no framework. Keep it that way unless Brad explicitly says otherwise — the simplicity is the elegance.

Since v0.4 the game grew a moral memory: everything is optional and everything is counted. Three silent verbs — kill/spare, take/pass, stop/keep-walking — drive multiple endings.

## Design laws (non-negotiable, in priority order)

1. **The game never names its subject.** No "addiction," "alcohol," "sober," "relapse" in any player-facing text. The player assembles the meaning; that's why it detonates.
2. **Every mechanic must double as metaphor, or it's cut.** Examples in place: tolerance ticks raise elixir drain (dependency escalates); walls break instantly buzzed or in ten sober hits (the sober way exists — slower, harder, real); enemies drop potions (the violence feeds the need feeds the violence); family enemies never strike, they only hold on and slow you (the player chooses violence against people who never hit them); no attack button in Act II (nothing left to fight); you can't die on the way back (you survive that part — that's the point); the bar temptation is beaten by *not stopping*.
3. **Add investment, not length.** Target stays ~5 minutes each way. If a change doesn't deepen the player's relationship with potions or with a loved one, it's padding.
4. **The way back is sacred.** Slow, gray, quiet, unwinnable, uninterruptible. Don't add challenge, collectibles, or pacing "improvements" to Act II. Its emptiness is the content.

## Architecture (all in potions.html, one <script>)

- Internal canvas 320×180 (`buf`/`bctx`), integer-upscaled to screen (`screen`/`sctx`), imageSmoothing off.
- **Text renders on a separate hi-res overlay**: queue via `T(str,x,y,size,col,align,alpha,bold)`, flushed by `flushText()` after the buffer blit. Never draw text into the low-res buffer.
- **Sprites**: palette-indexed pixel maps (`SPR_HEAD/TORSO/LEGS_*`, all rows exactly 12 chars — verify lengths if you edit them) rendered by `drawSprite` at 2× scale. `drawFigure(x,y,opts)` is the universal humanoid; `drawShadowMonster` wraps the *same body* in shadow — the reveal is literal.
- State machine: `title → act1 → turn → act2 → end`, driven in `frame()`.
- Global saturation `SAT` (0–1.2) desaturates every color drawn through `C(h,s,l)`. The buzz raises it, withdrawal and Act II crush it, the sober ending restores it. All world colors must go through `C()`.
- Key systems: `updateAct1` (movement, potion economy with avoid-counting, wall gates with sober HP, mob spawner — **only spawns after the first potion**, spare tracking, combat), `updateAct2` (the walk home, reveal holds, spared-vs-killed line selection, temptation system: `a2pots[]`, rubble pop, `barOffer` linger logic), `drawLandmarks` (same buildings, fantasy-skinned in Act I, real in Act II), `player.kills[]` (everyone killed stands in Act II), `player.avoided` / `resisted` / `e.spared` (mercy counters).
- **Sober state is systemic**: `potionsDrunk===0` means no mobs ever spawn, family renders as people (not shadows) in Act I, Act II reveal lines change, and the ending scene blooms back to color with the family at the house.
- **Day counter** persists via localStorage (guarded in try/catch — must never throw where storage is unavailable). "Walk it again" increments the day; taking a potion on the way back resets to day one.
- Audio: WebAudio, no assets. `MEL` is one 16-step melody — forward/square/146bpm + sparkle echo in Act I, **reversed**/triangle/60bpm + pad swell in Act II. Withdrawal detunes everything to 0.94. Craving below 25 elixir adds a literal heartbeat (`sfx("heart")` + vignette pulse). Audio inits on first keydown (browser autoplay policy).
- Named characters live in `LOVED` with paired `line` (killed) / `spared` text — Mom must remain the last figure before home. Generic crowd labels in `CROWD`.

## Tuning knobs (where the feel lives)

- Elixir drain: `3.2 + tol*1.35` in updateAct1 — the dependency curve.
- Power scaling: `power = min(potionsDrunk,16)` → speed `78+power*4`, damage `1+(power/3|0)`, jump, knockback, shake.
- Spawner: interval `max(0.7, 3.0 - x/1100 - power*0.09)`, cap 7 alive, 50% potion drop, gated on `potionsDrunk>0`.
- Pickup boxes: Act I potions x<8 / y<9 (a jump clears them — keep it that way); Act II temptations x<7 / y<8 against a −145 jump (clearable, barely — the margin is intentional).
- Sober wall: 10 hits at 0.45s cooldown. Spare distance: 90px past a family member.
- Bar offer: warns at 1.0s of lingering, takes at 3.4s. Escape by moving.
- Act II walk speed 40 (28 wounded-facing-right). Resist the urge to speed it up.

## Current state / known rough edges

- Sprites are 12×16 pixel maps at 2× — serviceable Shovel-Knight-adjacent, but loved ones share one body; distinct silhouettes for Mom/Grandma/Danny/Sarah is the biggest remaining visual win.
- The dog is still hand-drawn rects, not a sprite.
- Spared family members stand where they stopped chasing, not at their home positions — decide if that's a bug or the truth.
- Playtest tuning is unfinished — all numbers above are first guesses.
- The sober route is undiscoverable by design; consider whether day 3+ should hint at it.

## Endings matrix (verify all when touching act2/end code)

1. Drank + killed everyone: gray ending, kill/potion counts.
2. Drank + spared some: spared lines in Act II, "they remember" on the card.
3. Took one on the way back (any route): three seconds of color, "day one starts again," day resets.
4. Zero potions: no mobs ever spawn, family visible as people from the start, color blooms at home, family gathered — "They're all still here. They always were."

## The iteration protocol (how we know it's a gem)

The one metric: playtesters describe **the feeling of the turn** unprompted. If they talk about controls or combat first, fix investment, not features. Cut order when something drags: combat depth first, zone length second, loved ones never.

## Working with Brad

Brad is the designer; treat the emotional beats as spec, not suggestion. He values restraint — when in doubt, do less, and flag ideas as options rather than shipping them. Small, playable iterations beat big refactors. Before any structural change, ask: does this make the turn hit harder?

## Repo housekeeping

Files: `potions.html` (the game), `README.md`, `POTIONS-beat-map.md` (design doc), this file. Sensible first commits: init repo, then one commit per playable change with messages describing the *felt* change ("act II walk feels longer", not "adjusted constant").
