# POTIONS — Beat Map v2
*v0.4 state. One continuous world, ~5 minutes each way.*

---

## Design laws (the anti-overdoing rules)

1. The game never says "addiction," "alcohol," or "sober." Not once. The player assembles the meaning — that's why it detonates.
2. Every mechanic must double as metaphor, or it's cut.
3. No text moment longer than 7 lines.
4. Add investment, not length. If something doesn't deepen the player's relationship with potions or a loved one, it's padding.

---

## The world

One horizontal map, 2600px wide. Player starts at x:60 facing east. The light is at x:2550. Home is at x:30.

### Loved ones (west → east, Act I order)

These are shadow monsters on the way there. On the way back, they're standing exactly where you left them, and you can see their faces.

| Position | Name | Act II line |
|---|---|---|
| x:430 | MOM | "She was trying to take it from you." |
| x:820 | GRANDMA | "She just wanted you to stay for dinner." |
| x:1240 | DANNY | "Your brother. He called every Sunday, for a while." |
| x:1650 | SARAH | "She waited longer than anyone." |
| x:2050 | YOUR DOG | "He never understood why the walks stopped." |
| x:2350 | YOU | "This one was always the hardest fight." (6 HP, everything else is 3) |

Mom is first. You is last before the light.

### Landmarks (same buildings, two skins)

| Position | Act I (fantasy) | Act II (real) |
|---|---|---|
| x:500 | Castle keep | Your old school |
| x:1010 | Twin spires | The dorms |
| x:1700 | Dark tower | The office |
| x:2120 | The glowing den | The bar |

Labels only appear in Act II, when you're close enough to read them.

### The two gates

The level manufactures the need twice:

- **Walls** (x:700, x:1560) — stone walls that only break while buzzed. Hitting them sober plays a thud and says *"It won't break. Not as you are right now."* In Act II they're rubble underfoot.
- **Dark zone** (x:1150–1520) — the screen dims to near-black unless buzzed. Walking in sober triggers *"Too dark to see the path. Something in your bag is glowing."* In Act II it dims but doesn't stop you — it turns out you can walk through the dark. That's new information.

---

## ACT I — THE WAY THERE

### The elixir economy

- Drain rate: `3.2 + tolerance × 1.35` per second. Dependency escalates.
- Buzz: 3 seconds per potion. Raises color saturation, speed, jump.
- Withdrawing (elixir = 0): movement halved, jump reduced, HP bleeds, "You need another one." fires randomly.
- Tolerance ticks are shown as dots on the HUD labeled NEED. Drinking now just gets you back to normal.

### What potions do as they stack

| Potions drunk | Message |
|---|---|
| 1–2 | "Warmth." |
| 3–5 | "Everything is fine now." |
| 6–8 | "More." |
| 9–11 | "You feel amazing." |
| 12–14 | "Just one more after this." |
| 15+ | "It works. It always works." |

### The buzzsaw

Generic enemies spawn continuously, interval shortening as the player goes further east and drinks more. They drop potions 50% of the time. The violence feeds the need feeds the violence.

### The mob spawner

`interval = max(0.7, 3.0 - x/1100 - power × 0.09)`, cap 7 alive. Final surge of 6 enemies in the last stretch before the light.

### Death

HP → 0 respawns at last checkpoint (last potion pickup). "You wake up. First thought: potion." You can't escape the loop this way.

### Goal

Reaching x:2540 → THE TURN.

---

## THE TURN

Seven lines, player frozen at the light:

1. "You made it."
2. "The light you chased the whole way..."
3. "...is just a light."
4. "There are no potions here."
5. "There are no potions anywhere, anymore."
6. "The only way out is back the way you came."
7. "[ walk home ]"

Player presses J to advance each line. Then faces left.

---

## ACT II — THE WAY BACK

Same map, reversed. Half speed (40px/s west, slower if trying to go east). No attack button — pressing J says "You don't have the strength to fight. And there's nothing left to fight." No elixir meter — the UI has gone quiet. HP decays but floors at 8. You cannot die here. You survive this part. That's the point.

Color saturation: 0.16 (gray). The only saturated color in the world is the warm window at home.

### The reveals

Walking west, each loved one triggers their line as you pass their x-position. The order is the reverse of Act I. Mom is last, just before home.

### The crowd

Every generic enemy you killed is standing along the road home. Walk close and they show a label: "a friend from college," "your coworker," "your roommate," etc. No dialogue. Just standing there.

### The one choice

A potion sits at x:180, steps from home. Full color in the gray world. It's the only choice in the whole act.

- **Take it:** three seconds of color and warmth, then gray. End card changes.
- **Walk past:** nothing happens. No fanfare, no reward.

### Home

The warm window. Walk through the door (x:30) → THE END.

---

## THE END

Screen fades. Lines appear in sequence:

- "You made it back."
- "Not fixed. Not fine."
- "Just back. That's day one."
- **POTIONS** (title reveal, full color)
- "you drank N potions on the way there"
- "you went through N people to get to the light"
- If took it: "and you took one on the way back. day one starts again."
- If didn't: "you needed zero on the way back"

---

## How we know it's a gem (iteration protocol)

**The one metric:** playtesters describe *the feeling of the turn* unprompted. If they talk about controls or combat first, the firework fizzled — fix investment, not features.

**Cut order when something drags:** combat depth first, zone length second, loved ones never.

---

## What's not built yet

These are designed but not in v0.4:

- **The first potion as a choice** — right now it's just a bottle like the others. The design intent was a deliberate first offer: optional, framed like a toast, no cost visible yet.
- **The dog doesn't fight back** — currently it's a shadow monster like everyone else. The design intent: small, won't attack, but blocks the path. The player has to decide.
- **Sprite pass** — figures are chunky rect-humanoids. A 2-frame walk cycle and hurt flash are the biggest visual win available.
- **Platforming / LEAP mechanic** — gaps only clearable while buzzed was in the design but isn't in the world geometry yet.
