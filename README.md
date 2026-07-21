# BroMind model catalog

Starter-model suggestions for the [BroMind](https://github.com/bromind-ai) browser
extension's first-run wizard. The extension ships with a built-in copy of this
list; it fetches `starter-models.json` from this repository **only** when the
user explicitly clicks "Check for newer suggestions", and falls back to the
built-in list if the fetch fails or the file is invalid.

## `starter-models.json` schema

An array of up to 20 entries:

| Field | Type | Constraints |
|---|---|---|
| `id` | string | Ollama tag on the **default registry** — letters, digits, `.`, `_`, `-`, optional `:tag`. No slashes (custom registries are rejected by the extension). |
| `label` | string | Display name, truncated to 60 chars by the extension. |
| `minRamGb` | number | Approximate minimum machine RAM in GB for a comfortable experience. |
| `note` | string | One-line guidance, truncated to 200 chars. |

Entries that fail validation are dropped client-side; if none survive, the
extension uses its built-in list. Keep the smallest-RAM option first for
readability (the extension sorts by `minRamGb` regardless).

## Updating

Edit `starter-models.json` on `main`. The extension fetches the raw file
directly, so changes are live for users as soon as the commit lands — no
extension update required. Test a candidate list by validating it is plain
JSON (no comments, no trailing commas) before merging.
