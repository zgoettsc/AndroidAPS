# Offline Documentation Archives

Verbatim offline copies of the official documentation for the diabetes-rig apps, built for
grid-down use (open in any phone browser, searchable, no internet). Part of the SHTF loop
resilience kit — see `../SHTF_LOOP_RESILIENCE_PLAN.md`.

## Files here (committed)

| File | Contents | Source & license |
|---|---|---|
| `AAPS_Official_Docs_Archive.html` | All 121 English AAPS doc pages — incl. Omnipod DASH/Eros/Medtronic, Dexcom G7, xDrip, Juggluco, and the Bluetooth / General / Profile-Tuning troubleshooting | `openaps/AndroidAPSdocs` (readthedocs), **AGPL-3.0** — verbatim redistribution permitted |
| `xDrip_Official_Docs_Archive.html` | 25 pages — README, Quick Start, Incoming Glucose Broadcast, Watch Guide, wiki, technical docs | `NightscoutFoundation/xDrip` README + Documentation + wiki, **GPL/AGPL** |
| `Juggluco_Complete_Guide.html` | Every juggluco.nl help page + Juggluco README/wiki, AAPS-integration section first | Compiled from juggluco.nl + Juggluco GitHub (© Jaap Korthals Altes); included with attribution for personal reference |

The AAPS/xDrip archives are text-only (screenshots omitted to keep each a small single file); the
images remain in the upstream sources. Redirect/script tags have been stripped so the files never
navigate away.

## Related docs elsewhere in this repo

- `../FIELD_MANUAL.html` — operational + off-grid troubleshooting (this repo's own content).
- `../SETTINGS_REFERENCE.html` — the owner's current therapy settings (name-free), for offline
  viewing and tuning. Reference only; not dosing advice.

## Rebuilding / updating

Archives were generated from the upstream Markdown sources with a small converter
(`build_archive.py`, kept with the kit). To refresh: re-clone the source repos and re-run the
converter. Update whenever the upstream docs change materially.
