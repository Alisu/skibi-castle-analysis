# Skibi Castle — extracted analysis data

Reference data about the Warcraft III custom map **Skibi Castle TD**, read directly
out of the map file rather than transcribed from tooltips.

This is observation of someone else's map, kept as research notes. Nothing here is
map content — no models, sounds, scripts or assets — only measured numbers and the
game's own descriptive text.

## Layout

| Path | What |
|---|---|
| `champions/*.csv` | one file per champion — every tower with exact cost, damage, cooldown, dps, range, armour/attack types, traits |
| `champions/other_towers.csv` | towers present in the map that no champion file claims; the 3 attributable ones say which champion |
| `waves.csv` | every wave 1–44, one row per spawn slot (`main`, `a`, `b`) — hp, armour value + type, move type, speed, bounty |
| `wave_modifiers.csv` | each wave's modifier list (Oversoul, Mechanical, Flame …) for **all three game modes** |
| `bosses.csv` | named bosses with hp, armour, bounty |
| `armour_matrix.csv` | the WC3 armour × attack type multiplier grid the whole game runs on |
| `game_modes.csv` | Classic / IMPOSSIBLE / Turbo / Mini-Game — lives, score multiplier, what each changes |
| `glossary/tower_traits.csv` | what each tower trait does, quoting the map's own ability description |
| `glossary/wave_traits.csv` | what each wave modifier means |

## Two things to know before using the numbers

**`obs_` columns are eyeballed, everything else is read from the file.** Columns
prefixed `obs_` come from notes taken while playing — discovery order, commentary,
per-wave observations. Everything unprefixed is extracted. Where they disagree, the
extracted value is right: the hand capture had to guess attack cooldowns from the
in-game speed words ("very rapid", "rapid"), and **those guesses were wrong by up to
2.6×**, which is why the extraction exists.

**A blank means unknown, not zero.** 39 tower traits are stock Warcraft III abilities
the map never defines; those rows carry the raw ability id and an empty description
rather than a guess. Waves 43–45 are literally `??` in the map author's own text.

In `glossary/wave_traits.csv`, `derived_evidence` is **measured, not authored** — the
map names its wave modifiers but never defines them, so each is characterised by
comparing the waves that carry it against those that don't. `always_co_occurs_with`
names labels that ride on every wave a trait appears on, because that evidence can't
be attributed to one label alone.
