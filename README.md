# currents-vault

Tidal-gate reference data for the Pacific Northwest — the canonical source feeding
[`currents-mcp`](../currents-mcp). Public because the station identity comes from
open government current-prediction services and the hazard notes are paraphrased
facts, not reproduced text.

> ⚠️ **Not for primary navigation.** Timing and hazard notes are decision aids
> paraphrased from cruising references. Confirm slack and transit conditions against
> official CHS/NOAA current tables and current chart information before any passage.

## What this is

- `passes/<slug>.md` — one file per tidal gate. YAML frontmatter carries a `station`
  key naming the gate's entry in
  [`@sailingnaturali/station-corrections`](https://github.com/sailingnaturali/station-corrections)
  (which owns the name, position, provider and provider station id), plus this vault's
  own knowledge: `transit_window_minutes` and a `hazards` list. The markdown body holds
  free-form route context. Hazards are **state-first** — each entry names when it
  applies (`flood`, `ebb`, or `any`) and where the danger is.
- `destinations.yaml` — routing table: each destination's aliases and its ordered
  gates, as station-registry keys. Open-water destinations have an empty gate list
  by design.
- `manifest.yaml` — source provenance and licensing.

## How it's consumed

`currents-mcp` reads this directory via the `CURRENTS_VAULT_PATH` environment
variable (default `~/.currents-vault`). Gate keys in `destinations.yaml` must match a
`passes/<slug>.md` `station`, and every `station` must exist in the registry; the
loader fails loudly on a mismatch or malformed file. Because routing is by registry
key, renaming a gate is a one-file edit in `station-corrections` — nothing here moves.

## Contributing hazards

Add a `hazards` entry to the relevant `passes/*.md` file, keyed to the current state
it applies to, and record your source in `manifest.yaml`. Paraphrase — do not paste
copyrighted guide text. Northern-rapids notes here are drawn from the 48°North piece
*"Transiting the Passes to Get You Beyond Desolation Sound"*; most other gates carry
no hazard notes yet and are good first contributions.
