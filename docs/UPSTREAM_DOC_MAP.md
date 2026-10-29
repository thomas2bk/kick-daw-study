# Upstream document map

What Music Tribe actually shipped as “docs” in `0700-AAM` @ `27194180`.

## Inventory

| Path | Role | Depth |
|---|---|---|
| Root `README.md` | Product pitch, feature bullets, rear/front I/O table, folder → license matrix, Discord + CONTRIBUTING + security advisory links, trademark disclaimer | Marketing + legal entry |
| `docs/images/*` | Social preview, front/rear photos, multi-view renders | Visual only — **no prose architecture** |
| `Kick/README.md` | JUCE app license, **build will not work OOTB**, removed content list, third-party license table | Engineering honesty |
| `Kick/how-to/Kick_Compilation.txt` | WSL/Linux local build, Buildroot, cross-compile via `toolchainfile.cmake` | Procedural, sparse |
| `AudIO/README.md` | Engine elevator pitch (patchable graph, buses, chains, small DAW layer, Airwindows), removed SoundFont/samples, third-party table | Best technical README |
| `ComProtocol/README.md` | One paragraph: framed USB packets (header, type, payload, CRC) | Minimal but clear |
| `Linux/README.md` | Buildroot board/config names, NXP license prompts, **dev image has passwordless root + Dropbear** | Security warning done right |
| Org `CONTRIBUTING.md` (linked, not in-tree) | PR / Discord contribution path | Community ops |

## What is missing (and that absence is a signal)

No published:

- Product user manual / workflow guide
- Flash / recovery / OTA procedure
- Supported toolchain versions pinned in prose
- Emulator / panel simulator runbook (though `kickem` exists as a build flag)
- AI camera API or gesture model docs (feature is marketed; code/docs absent)
- Formal IPC message catalog for integrators
- Schema for project / program files
- Latency / RT guarantees
- Audio graph diagram beyond README prose

**Lesson:** Open-sourcing a tree is not the same as documenting an instrument. The READMEs document **repositories and licenses** far better than **musical workflows**.

## Folder = product surface

Root README’s table is the strongest doc artifact:

```text
Kick/         Application          AGPL-3.0-or-later
AudIO/        Audio engine library AGPL-3.0-or-later
ComProtocol/  Hardware protocol    AGPL-3.0-or-later
Linux/        Buildroot image      GPL-2.0 (Buildroot)
```

Readers can navigate by **concern** without opening CMake. That is the doc pattern worth stealing for MPCX study repos and for any future open surface MPCX might expose.
