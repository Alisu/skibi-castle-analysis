# `Skibi'sCastleTD 2.3` — patch notes vs the baseline

*Diffed from the map files, not from play. Every line below is a real difference.*

---

## At a glance

> **No balance changes.** Credits replaced, and standard melee start units added per
> player. Its own changelog makes two claims the file does not support.

| | |
|---|---|
| Towers | **0** changed, 0 added, 0 removed |
| Waves | **0** changed |
| Wave modifiers | **0** changed |
| Minigame rewards | **0** changed |
| Hero abilities | **0** changed |
| Bosses | **0** changed |
| Items | **0** changed |

---

## What it says about itself

The map ships a changelog string:

```
- Up Gold per 10 sc
- New Tower
- Web : http://www.webalfa.org
- Email : aliking@webalfa.org
```

**Both gameplay claims are contradicted by the file.**

- **"New Tower" — there is none.** `war3map.w3u` (every unit and tower) and
  `war3map.w3a` (every ability) are **byte-identical** to the baseline. No tower type
  was added, removed or edited, and the champions' buildable lists are unchanged.
- **"Up Gold per 10 sc" — no gold logic changed.** Every gold award in the script is
  the same set of amounts as the baseline, to the value. What *was* added is a **gold
  mine holding 1,000,000 gold for each of the 10 players** (see below), which is
  presumably what the line refers to — but it is a preplaced unit, not a change to the
  income rules.

## Attribution

- Title: `"Skibi's Castle TD"` ⇒ `"Skibi's Castle TD 2.3 Ver WebALfa"`
- Author: `"Cerrada-- and Blizzard Entertainment"` ⇒ `"AliKing & AminGod"`
- `"BY: CERRADA--  PRESENT"` ⇒ `"Skibi's Castle TD 2.3"`
- `"CLASTLE TD SKIBI's"` ⇒ `"WwW.WebALfa.OrG"`
- Map description ⇒ `"Official Blizzard version of the popular TD with a mini-…"`

## Map setup — the only real mechanical difference

Standard Warcraft III **melee starting units** were added for all ten players, and the
start locations moved:

| | baseline | 2.3 |
|---|---|---|
| Gold mines | 0 | **10** (one per player, **1,000,000 gold each**) |
| Castles (`hcas`) | 0 | **10** |
| Workers | 0 | **10** |
| Town-bell order issued | no | yes |

Player 0's hall also moves from `(-5312, 5312)` to `(2752, -8960)`.

- **+10 functions** — `CreateUnitsForPlayer0…9`
- **−18 functions** — the old `Trig_Initialize_Players_*` helpers
- **17 changed** — `CreateBuildingsForPlayer0…9`
- JASS **+1826 bytes**

## Read

This is the signature of a map **opened in the World Editor and re-saved with melee
settings on**: the editor generates the standard start-location kit (hall, workers, gold
mine) and rewrites the placement functions. It is not a designed change — nothing about
the tower defence itself was touched.

Whether the 1,000,000-gold mine is reachable in play is **unverified**: it is placed, but
the TD rules never reference it. If it *is* reachable, it would trivially break the
economy, which is worth one minute of checking before anyone plays this version.
