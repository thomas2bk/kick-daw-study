# ComProtocol notes

Source of truth in upstream: `ComProtocol/PktMgr` (~380 LOC) + one-paragraph README.

## Frame idea (from README + public headers)

Framed packet over USB:

```text
[ start / header fields ][ type ][ dir ][ id ][ size ][ payload ][ CRC ]
```

Receiver is a small state machine (`INIT_1` → … → `DATA` → `CRC` → `EOF`).

## Packet types (public enum)

| Type | Likely payload domain |
|---|---|
| SYSTEM | Bring-up / housekeeping |
| BUTTON | Faceplate buttons |
| LED | Pad / button illumination |
| PAD | Velocity / pad events |
| KNOBS | Assignable knobs / jog |
| MIDI | Bridged MIDI |
| CV | CV / Gate |
| SLIDER | Touch strip |

Direction: **REQUEST** vs **RESPONSE**.

## Doc quality

ComProtocol’s README is short but accurate: it states channel (USB), framing responsibilities, and dependency stance (no external deps). The **type enum is the real protocol doc**.

## Lessons for MPCX

MPCX already documents host↔client messages in `CONTROL_PROTOCOL.md` (WebSocket JSON). Parallel ideas:

1. Keep a **typed message taxonomy** (transport / pads / Q-Link / parameter / clip_state) in one table.  
2. Separate **panel/hardware encoding** (MIDI map docs) from **project-state protocol**. KICK’s split is ComProtocol vs IPC JSON — same spirit.  
3. If MPCX ever speaks a binary panel protocol (unlikely for original MPC X), publish frame + CRC + version like ComProtocol — but prefer versioned JSON schemas for workspace clients.
