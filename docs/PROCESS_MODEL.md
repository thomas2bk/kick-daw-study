# Multi-process model

Inferred from public Kick contracts (`ipc_config_constants.h` and app names). Ports are the **documented-in-code** service map.

## Processes

| Host ID | Process | Role | Server port |
|---:|---|---|---:|
| 5 | Kick Main | Supervisor / heartbeats / exit / logging hub | 50101 |
| 3 | KickDeviceControl (DCL) | Hardware events → IPC (pads, knobs, LEDs, …) | 50201 |
| 1 | KickAudioEngine | RT / graph process | 50301 |
| 2 | KickAudioModel | Project / program model | 50401 |
| 4 | KickUserInterface | Touch UI | (connects to others) |

Optional build products: `kickem` (simulator), `kickvst`, `midiPort`, multitouch helper.

## Connection graph (from named connection IDs)

```text
                    ┌──────────────┐
                    │  Kick Main   │ :50101
                    └──────┬───────┘
           ┌───────────────┼───────────────┐
           │               │               │
           ▼               ▼               ▼
    DeviceControl    AudioEngine     AudioModel
        :50201          :50301          :50401
           ▲               ▲               ▲
           │               │               │
           └───────┬───────┴───────┬───────┘
                   │               │
                   └─────── UI ────┘
```

IPC is described as **async JSON messages**; senders decide whether to block. Heartbeat handlers live under `kick_main`.

## Why this matters for docs / design

1. **Crash isolation** — UI death ≠ necessarily audio death (aspirational; depends on implementation quality).  
2. **Clear public names** — process + port constants are a contract other tools can target.  
3. **Hardware as a peer** — DCL is not buried inside the UI binary; panel I/O is its own service.  
4. **Model vs engine** — project state process separate from audio engine process (rhymes with MPCX Project State Server vs AudioGraph, even though MPCX keeps them in-process today).

## MPCX comparison (high level)

| Concern | KICK | MPCX (today) |
|---|---|---|
| Hardware I/O | DCL process + ComProtocol USB | CoreMIDI / ACVS / HostSurface in host |
| Authoritative state | KickAudioModel (+ IPC) | Project State Server (in-process → WebSocket clients) |
| Audio | KickAudioEngine + AudIO | JUCE / CoreAudio + AudioGraph |
| UI | KickUserInterface process | Simulator / future iPad / browser clients |
| Isolation | OS processes + TCP ports | Threads + RT queues; multi-*client* not multi-*process* |

MPCX does not need to clone the five-process Linux layout. The **lesson** is: name the planes and document how they talk.
