# AudIO / DAW stack (from docs + public headers)

## AudIO README claim

> Patchable graph of audio objects (oscillators, ADSR, mixer, playback and recorder, SoundFont synth, Airwindows effects) with buses, chains and a small DAW layer. Usable as a JUCE module or via CMake. Examples under `AudIO/Example/`.

That single paragraph is the best technical documentation in the release.

## Layers

```text
DawEngine  (sequences, tracks, transport helpers, preview, recorder hooks)
    └── Design  (createObject / createChain / createBus / patch / inserts / meters)
            └── Object graph  (DSP leaves + Airwindows + SF synth + I/O devices)
```

### Design (graph core)

Public surface emphasizes:

- Create/remove named objects by type string  
- Chains and buses with send amounts / input gains  
- Inserts on chain-or-bus with positional add/remove  
- Patch / unpatch (including per-channel)  
- Nested Designs (`insertDesign`)  
- Meter attach / read  

This is closer to a **modular host** than to a classic track-only DAW mixer.

### Daw\* (small DAW layer)

| Type | Responsibility |
|---|---|
| `DawEngine` | Owns bus manager; sequence CRUD; play/stop/pause; previews; recorder API |
| `DawSequence` | Named container of tracks + transport state |
| `DawTrack` | Name + mute/solo (thin — much voice logic lives in Kick `audio_program`) |
| `DawBus` / routing / inserts | Mixer-facing bus with gain/pan/mute/solo and insert slots (max inserts constant) |
| `DawTime` / notes | Timing helpers for the sequence layer |

### Kick engine programs (application side)

Under `Kick/modules/engine/audio_program`, program kinds mirror classic MPC vocabulary:

- Drum / Keygroup / Clip / Audio / MIDI / CV programs  
- Voice classes (`drum_voice`, keygroup, clip, audio preview, metronome)

UI edit surfaces under `program_edit_ui` follow the same nouns (`drum`, `keygroup`, `clip`, `audio`, `midi`, `cvgate`).

**Doc lesson:** nouns are consistent across engine + UI folders even without a formal data-model markdown file. Folder names *are* the schema outline.

## Examples as documentation

`AudIO/Example/` includes BasicUsage, DynamicPatching, Subdesign, Synth, Daw — README points here instead of writing a book. Pattern: **executable docs over prose**.

## Comparison to MPCX AudioGraph

| | AudIO Design | MPCX AudioGraph (Phase 1) |
|---|---|---|
| Compile model | Live object IDs + patch | Control-thread compile → RT `PublishedGraph` |
| Leaves | Built-in Objects + Airwindows | AU/VST3 + first-party native inserts |
| Mixer | DawBus / sends / submix / aux | Track → bus sum + sends + AFL cue |
| Extensibility | String `createObject(type)` | Plugin host + native DSP library |
| Docs | README + examples | `AUDIO_GRAPH.md` + tests |

MPCX should keep RT compile/publish discipline. Worth borrowing: **example apps as living docs** and **clear bus-type vocabulary** in prose.
