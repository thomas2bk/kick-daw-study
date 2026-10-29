# Lessons for MPCX

Actionable takeaways from KICK’s **documentation posture** and the architecture those docs describe. Not a mandate to clone their stack.

## Steal (docs)

1. **Folder → concern → license table** on the repo front page.  
2. **Hardware I/O table** next to software layout (MPCX: keep `HARDWARE.md` linked high in README).  
3. **“Won’t work yet”** called out beside Build & run — same honesty as Kick’s OOTB warning.  
4. **Removed / not redistributed** lists whenever content can’t ship (samples, fonts, proprietary bridges).  
5. **Security notes** when any network listener exists (WebSocket project server, future LAN).  
6. **Examples as docs** — small host binaries that demonstrate AudioGraph / HostSurface beats long essays alone.  
7. **Stable nouns** across UI + engine folders (Kick: drum/keygroup/clip). MPCX play types + instrument targets should stay equally consistent in docs and code paths.

## Steal (architecture ideas — clean-room)

1. **Name the planes:** hardware I/O · project model · audio engine · UI/clients. MPCX already has this; keep docs aligned when Distributed Workspaces grow.  
2. **Hardware as a peer service** — HostSurface should remain swappable (MPC X today, other surfaces later) the way DCL is a peer process.  
3. **Typed panel taxonomy** — pads / knobs / strip / transport / system — mirrors ComProtocol enums; keep MIDI map docs in that shape.  
4. **Bus vocabulary in prose** — in/out/send/submix/aux language helps mixer docs stay legible.  
5. **Program kinds as first-class** — drum vs keygroup vs clip mental model is what users expect from MPC-shaped gear; MPCX sequencing/play-type docs should keep mapping those nouns to tracks/devices.

## Don’t steal

1. **AGPL application or AudIO code** into MPCX (see [LICENSE_BOUNDARY.md](LICENSE_BOUNDARY.md)).  
2. **Ship-thin, community-finishes** as a product strategy — MPCX’s bet is a finished Mac production engine + durable Akai surface.  
3. **Marketing features without a doc/code surface** (AI camera).  
4. **Passwordless networked images** as anything but a labeled lab build.  
5. **Five TCP microservices on device** unless isolation pain appears — prefer clear modules + RT queues first.

## Competitive read (market)

KICK @ ~$150 open clone pressure validates **MPC-shaped play** as a category. MPCX should double down on:

- Reliability and session depth of a Mac DAW  
- Real Akai pads / Q-Links as the performance contract  
- Multi-client workspaces KICK’s single 7″ panel cannot match  

Use this study repo to track upstream doc changes (`README`s, how-to, license tables) — not to absorb their firmware.
