# Architecture readable from the docs

What a careful reader can infer **from READMEs alone**, before opening headers.

## System sketch (from folder + Kick/AudIO READMEs)

```text
┌─────────────────────────────────────────────────────────────┐
│  Linux (Buildroot) — i.MX 8M-class SOM, USB gadget / panel  │
└───────────────────────────────┬─────────────────────────────┘
                                │ USB framed packets (ComProtocol)
┌───────────────────────────────▼─────────────────────────────┐
│  Kick (JUCE application tree)                               │
│    UI · device control · audio model · engine host apps     │
└───────────────────────────────┬─────────────────────────────┘
                                │ links / uses
┌───────────────────────────────▼─────────────────────────────┐
│  AudIO — patchable Object graph                             │
│    buses · chains · inserts · meters · small Daw* layer     │
│    Airwindows FX catalog · SF synth · playback/record       │
└─────────────────────────────────────────────────────────────┘
```

## Claims the docs make

| Claim | Source |
|---|---|
| App is C++ / JUCE | `Kick/README.md` |
| Engine is a **patchable graph** of audio objects | `AudIO/README.md` |
| Graph supports **buses, chains**, and a **small DAW layer** | `AudIO/README.md` |
| 300+ Airwindows effects in-tree | `AudIO/README.md` + marketing bullets |
| Hardware link is **USB framed packets** with CRC | `ComProtocol/README.md` |
| Target OS image is **Buildroot**, Freescale/Variscite board configs | `Linux/README.md` |
| Simulator / VST / MIDI port are **optional CMake products** | implied by Kick app layout (named in tree; README focuses on main gaps) |

## Separation of concerns (the useful idea)

Docs encode a four-way split that maps cleanly onto any hardware DAW:

1. **OS image** (Linux/) — board bring-up, not musical logic  
2. **Panel protocol** (ComProtocol/) — bytes on the wire  
3. **Application / UX** (Kick/) — JUCE UI + orchestration  
4. **DSP / graph** (AudIO/) — reusable engine library with examples  

MPCX already splits Mac host / HostSurface / AudioGraph differently (controller-mode hardware, not embedded Linux), but the **documentation posture** — name each concern and license it — is portable.

## JAM DAW naming

Marketing and GitHub blurb call the software **Music Tribe JAM DAW**. AudIO’s README is more precise: engine + “small DAW layer” (`DawEngine`, sequences, tracks, buses). Treat “JAM DAW” as the product OS brand; treat AudIO Daw\* as the actual documented engine surface.
