# Concept: Forge Incremental Log

**Status**: READY
**Complexity**: MODERATE
**Created**: 2026-04-07
**Updated**: 2026-04-07

## Summary

Forge currently writes the concept file only at session boundaries — once on bootstrap (EXPLORING) and once when the concept reaches READY. If a session is interrupted mid-way, all in-session progress is lost. This concept makes the concept file a live log: after every exchange, forge rewrites the upper sections (Summary, Accepted, Blocked, Discarded, Open Questions) to reflect the current state. The "Ready for Architecture" section is only written when the concept reaches READY status — its absence signals the concept is still EXPLORING. The bootstrap initial write remains a distinct step that precedes the per-turn update loop. Sessions are resumable at any point with no progress lost.

---

## Accepted

- **Problem**: Mid-session interruptions lose all in-session concept progress
- **Solution**: Rewrite upper sections (Summary, Accepted, Blocked, Discarded, Open Questions) after every turn
- **READY trigger**: "Ready for Architecture" section is written only when concept reaches READY — its absence signals EXPLORING
- **Section split**: Upper sections = live log updated every turn; "Ready for Architecture" = written once, at READY
- **Bootstrap write is separate**: The initial EXPLORING file write on bootstrap remains a distinct step before the per-turn update loop begins

---

## Blocked

*(none)*

---

## Discarded

*(none)*

---

## Ready for Architecture

**Concept summary**: Forge adds a per-turn file update step to its exchange loop. After every user response, it rewrites the upper sections of the active concept file (Summary, Accepted, Blocked, Discarded, Open Questions) with the current state. The bootstrap initial write (EXPLORING) remains a separate, prior step. The "Ready for Architecture" section is only appended when the concept is marked READY, making its presence or absence a reliable status signal. This eliminates progress loss from interrupted sessions and makes the concept file a live, resumable log throughout the entire session.

**Key constraints**:
- Bootstrap initial write is distinct and unchanged — it still precedes the per-turn loop
- Only upper sections are rewritten per turn — "Ready for Architecture" is not touched until READY
- The "Ready for Architecture" section is written exactly once: at the READY transition

**Confirmed directions**:
- Per-turn full rewrite of upper sections (not partial/diff updates)
- Section split: live log sections vs. architect handoff section
- Bootstrap remains a separate step

**Discarded alternatives**:
*(none explored — concept was clear and converged quickly)*

**Blocked (deferred)**:
*(none)*

**Open questions for the architect**:
- None — concept is fully specified
