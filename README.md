# currents-vault

Tidal-gate reference data for the Pacific Northwest — the canonical source feeding
[`currents-mcp`](../currents-mcp). Public because the station identity comes from
open government current-prediction services and the hazard notes are paraphrased
facts, not reproduced text.

> ⚠️ **Not for primary navigation.** Timing and hazard notes are decision aids
> paraphrased from cruising references. Confirm slack and transit conditions against
> official CHS/NOAA current tables and current chart information before any passage.

## What this is

- `passes/<slug>.md` — one file per tidal gate. YAML frontmatter carries the machine
  data (`provider`, `station_id`, `latitude`/`longitude`, `transit_window_minutes`,
  and for NOAA stations `noaa_bin`) plus a `hazards` list; the markdown body holds
  free-form route context. Hazards are **state-first** — each entry names when it
  applies (`flood`, `ebb`, or `any`) and where the danger is.
- `destinations.yaml` — routing table: each destination's aliases and its ordered
  gates. Open-water destinations have an empty gate list by design.
- `manifest.yaml` — source provenance and licensing.

## How it's consumed

`currents-mcp` reads this directory via the `CURRENTS_VAULT_PATH` environment
variable (default `~/.currents-vault`). Gate names in `destinations.yaml` must match
a `passes/<slug>.md` `name`; the loader fails loudly on a mismatch or malformed file.

## Contributing hazards

Add a `hazards` entry to the relevant `passes/*.md` file, keyed to the current state
it applies to, and record your source in `manifest.yaml`. Paraphrase — do not paste
copyrighted guide text. Northern-rapids notes here are drawn from the 48°North piece
*"Transiting the Passes to Get You Beyond Desolation Sound"*; most other gates carry
no hazard notes yet and are good first contributions.
