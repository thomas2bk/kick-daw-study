# Kick DAW Study

Clean-room notes on what **Behringer KICK** (`MusicTribeOpenSource/0700-AAM`) documents publicly — and what those docs imply for open music hardware and for **MPCX**.

This repo does **not** vendor Music Tribe source. Upstream is AGPL-3.0-or-later. Study notes here are original writing under MIT.

| Upstream | Snapshot studied |
|---|---|
| https://github.com/MusicTribeOpenSource/0700-AAM | `27194180` (2026-10-15) |

## Why this exists

MusicRadar framed KICK as “vibe-coded firmware” + open resources. The published **docs** (mostly READMEs + a short how-to) are thin on product UX, but unusually honest about **build reality**, **license boundaries**, and **process topology**. That honesty is useful even when the marketing is loud.

## Docs in this repo

| Doc | Focus |
|---|---|
| [docs/UPSTREAM_DOC_MAP.md](docs/UPSTREAM_DOC_MAP.md) | What they published vs what they didn’t |
| [docs/DOC_CRAFT.md](docs/DOC_CRAFT.md) | Documentation patterns worth copying |
| [docs/ARCHITECTURE_FROM_DOCS.md](docs/ARCHITECTURE_FROM_DOCS.md) | Architecture readable from READMEs alone |
| [docs/PROCESS_MODEL.md](docs/PROCESS_MODEL.md) | Multi-process IPC map (from public contracts) |
| [docs/PROTOCOL_NOTES.md](docs/PROTOCOL_NOTES.md) | USB ComProtocol packet types |
| [docs/AUDIO_STACK.md](docs/AUDIO_STACK.md) | AudIO / Daw layer shape |
| [docs/LESSONS_FOR_MPCX.md](docs/LESSONS_FOR_MPCX.md) | Actionable takeaways for MPCX |
| [docs/LICENSE_BOUNDARY.md](docs/LICENSE_BOUNDARY.md) | AGPL study rules — what we can / cannot do |

## Quick verdict

**Learn from their docs:** folder-as-product, license tables, “won’t build OOTB” honesty, process names + ports as a public contract.

**Do not copy:** AGPL application/engine code into MPCX; incomplete open dumps as a substitute for a finished instrument.

## Local upstream (optional)

```bash
git clone --depth 1 https://github.com/MusicTribeOpenSource/0700-AAM.git vendor/0700-AAM
# vendor/ is gitignored — keep AGPL trees out of this study repo
```

## License

Study notes: [MIT](LICENSE). Upstream KICK/AudIO/ComProtocol remain MUSIC Tribe AGPL-3.0-or-later. Behringer / KICK names are trademarks.
