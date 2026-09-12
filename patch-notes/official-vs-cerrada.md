# `(10)Skibi'sCastleTD` vs our baseline

*Diffed from the map files. **Corrected 2026-09-12** — the first version of this page had
the direction of the change backwards.*

---

## At a glance

> **No gameplay changes**, and `(10)` is almost certainly the **earlier, more original**
> file. Our baseline is the one carrying added credits.

| | |
|---|---|
| Towers · waves · modifiers · minigames · heroes · bosses · items | **0 changed** |

`war3map.w3u`, `war3map.w3a` and `war3map.w3t` are byte-identical, so no stat differs.

---

## Which came first — the evidence says `(10)` did

| | `(10)` | our baseline | `2.3` |
|---|---|---|---|
| editor save counter | **4473** | 4478 | 4484 |
| editor version | 6051 | 6051 | 6052 |
| string count | 2979 | **2982** | 2982 |

The `saves` field in `war3map.w3i` increments on every save in the World Editor, and
`(10)` has the **lowest count**. Independently, **`(10)`'s string table is a strict
subset of the baseline's**: the baseline holds three strings `(10)` does not, and `(10)`
holds *none* the baseline lacks.

Both point the same way: **the baseline is derived from `(10)`, by adding credits.**

## What the baseline adds

- `"BY: CERRADA--  PRESENT"`
- `"CLASTLE TD SKIBI's"`
- `"Made in Cerrada-- … clastle td skibi is present by Cerrada-- and blizza…"`
- Description: `"Official Blizzard version of the popular TD with a mini-game"` ⇒ `"By : Cerrada--green td skibi is presented by Closed…"`
- Author: `"Blizzard Entertainment"` ⇒ `"Cerrada-- and Blizzard Entertainment"`

## Script

One function differs, `InitCustomTriggers`, and it is **a no-op**: two registration calls
swap order.

```
  call InitTrig_TURBO_MODE_WIN()
+ call InitTrig_Skibi_Score_Calculations_E()
  call InitTrig_Skibi_Score_Calculations_W()
- call InitTrig_Skibi_Score_Calculations_E()
```

Same 430 lines, same calls, different order — what the editor emits on a re-save. The
remaining −10 bytes are the three removed strings.

---

## Read

**The "Official Blizzard version" line is plausibly genuine**, not a false claim as this
page first asserted. Blizzard did bundle community TD maps with later Warcraft III
builds (owner's recollection), and the `(N)MapName.w3x` filename is Blizzard's own
melee-map convention for player count. On the file evidence, `(10)` is the earlier
artifact and **our baseline is the re-branded copy**.

⚠️ **This does not affect the dataset.** Every stat table is byte-identical, so all
extracted numbers hold for both files. It only changes which file we should call
canonical — and on current evidence that is `(10)`, not ours.
