# Documentation craft — patterns worth copying

Observations about *how* KICK is documented, not about shipping quality.

## 1. Lead with hardware identity, then software folders

Root README opens with product name, photos, feature bullets, and a connections table **before** the source tree. Software people still get a clear hardware contract (MIDI DIN, CV/Gate ×4, USB-C/A, LINK RJ45, SD, stereo I/O).

**Steal for MPCX:** keep `HARDWARE.md` / MIDI maps as first-class “docs that ship with the story,” not buried after architecture essays.

## 2. License table on the front page

Every major folder README repeats: SPDX identity, what was **removed**, third-party table with path + license.

That reduces “can I use this?” thrash. AGPL still bites for derivatives, but the **inventory** is excellent.

**Steal:** when documenting first-party plugins / bridges, ship a one-screen dependency + license matrix.

## 3. Explicit “will not build out of the box”

`Kick/README.md` leads Building with failure modes:

- Private deps expected via `MT_PLATFORM_GIT_PATH` (even though AudIO/ComProtocol folders exist — docs lag the dump)
- Cross SDK must be produced from Buildroot
- Exact JUCE version + patch name

Honesty here is rarer than marketing “open source.” It sets contributor expectations and protects the brand from “broken clone” headlines *somewhat*.

**Steal:** MPCX Phase docs should keep a short **Known gaps / won’t work yet** block near Build & run (README already does this lightly — keep it sharper).

## 4. Security callouts in the Linux README

Passwordless root + enabled SSH called out as **development-only**. That single paragraph is better risk communication than many commercial firmware notes.

## 5. Community paths are first-class links

Discord, CONTRIBUTING, private security advisories — standard, but present. Security route is especially important once vibe-coded forks flash devices.

## 6. Trademark carve-out

Closing block: brand names/logos not covered by software licenses. Clean separation of code license vs product identity.

## 7. What *not* to copy from their doc craft

| Weakness | Why it hurts |
|---|---|
| `docs/` is images only | No architecture diagrams, no message IDs, no recovery |
| How-to is a raw `.txt` | Unstructured, WSL-centric, easy to rot |
| Feature marketing ahead of code | “AI camera” in bullets with no doc surface |
| No versioned protocol doc | ComProtocol is code-as-spec |
| No “official firmware baseline” promise | Community cannot tell MVP vs science project |

**Doc craft takeaway for an open instrument:**  
Ship **(A)** hardware I/O contract, **(B)** license matrix, **(C)** build truth, **(D)** flash/recovery, **(E)** protocol/schema versions — before inviting AI-generated forks.
