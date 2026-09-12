# Skibi Castle — version comparison

Four `.w3x` files were collected. Two are the same file, so there are **three** to compare:

| file | saves | md5 | verdict |
|---|---|---|---|
| `(10)Skibi'sCastleTD.w3x` | **4473** | `089d9030…` | ⭐ **CANONICAL** — earliest, official Blizzard-bundled build |
| `CLASTLE TD SKIBI.w3x` | 4478 | `405c50d7…` | the "Cerrada--" re-brand; what this dataset was first extracted from |
| `CLASTLE TD SKIBI(1).w3x` | 4478 | `405c50d7…` | byte-identical duplicate of the above |
| `Skibi'sCastleTD 2.3.w3x` | 4484 | `d5bf5181…` | the "WebALfa" re-brand, + melee start units |

**Lineage** (from the editor save counter, which only ever increments):

```
(10) official  4473  ──▶  CLASTLE TD SKIBI  4478  ──▶  Skibi's Castle TD 2.3  4484
                          + "Cerrada--" credits       credits replaced again,
                                                      + melee start units
```

2.3 *changes* the three Cerrada strings rather than adding them, so it descends from the
re-brand, not from the official file directly.

## The headline

**None of these is a balance patch.** The three data tables that hold every stat —
`war3map.w3u` (units and towers), `war3map.w3a` (abilities), `war3map.w3t` (items) —
are **byte-identical across all three maps**:

```
war3map.w3u   51c4a8d24a   51c4a8d24a   51c4a8d24a    SAME
war3map.w3a   c40380f1db   c40380f1db   c40380f1db    SAME
war3map.w3t   e49ddbcf70   e49ddbcf70   e49ddbcf70    SAME
war3map.wts   9ca440c793   2d2b2d50c7   a4cf4455df    differs
war3map.j     2a3cb945d9   437978e6f6   b25f327feb    differs
```

So **every number in this dataset is valid for all three files**: no tower cost, no
damage, no range, no wave HP, no bounty, no minigame reward and no ability changed.
The differences are confined to the string table and the script.

That is worth knowing before spending time re-extracting: running the full pipeline on
the other two maps produces the same CSVs, which we verified rather than assumed.

## Which file is canonical

On the file evidence, **`(10)` is the earliest of the three** — lowest editor save counter
(4473 vs our 4478 vs 2.3's 4484), and its string table is a strict *subset* of ours. Our
baseline adds three "Cerrada--" credit strings and nothing else. So the map we have been
calling the baseline is itself a re-branded copy, and `(10)`'s "Official Blizzard version"
description is plausibly genuine — Blizzard did bundle community TD maps with later
Warcraft III builds, and `(N)MapName.w3x` is Blizzard's own naming convention.

This changes nothing about the data: every stat table is byte-identical across all three.

## Per-version notes

- [`official-vs-cerrada.md`](official-vs-cerrada.md) — official ⇒ the `CLASTLE TD SKIBI` re-brand
- [`webalfa-23-vs-official.md`](webalfa-23-vs-official.md) — official ⇒ `2.3`

## How these were made

`tools/skibi-extract/patch_notes.py` diffs two extracted datasets and writes the
CSV-level differences. With the stat tables identical it now reports **0 changes in
every category**, and the real differences had to be read from the script and string
table directly.

**A tool that reports "no changes" is only trustworthy once you check what it was
looking at.** Two artifacts had to be removed before that zero meant anything:

1. it reported *"26 towers removed"* — the baseline carries an `other_towers.csv` that
   no extractor produces (it was built once by `consolidate.py`);
2. then *"12 towers added"* — rows marked `hand capture only`, preserved from play notes
   rather than read from the map.

Both are now excluded, and the omission is stated in the output rather than silent.
