# Concept: Forge Path and Decomposition

**Status**: READY
**Complexity**: MODERATE
**Created**: 2026-04-07
**Updated**: 2026-04-07

## Summary

Two enhancements to the forge skill. First, all concept file paths are standardized from `docs/concept/` (singular) to `docs/concepts/` (plural) relative to each project's repository root — every hardcoded path reference in the skill's startup sequence, process steps, and document examples must be updated. Second, the forge concept document schema is replaced with a new unified format: it adds a BLOCKED top-level status, a SIMPLE complexity tier, [CRITICAL]/[DEFERRED] tags in the Blocked section, and a Sub-concepts section for COMPLEX concepts. When forge assesses a concept as COMPLEX — or when the user explicitly requests it — forge decomposes the concept into named sub-concepts, each tracked with its own status (EXPLORING | READY | BLOCKED) and detailed notes. Sub-concepts are sections within the parent file, not separate files. They are mutable throughout the session (the concept log is live), and precise enough that the user can promote any sub-concept to its own forge session. The user decides if and when a sub-concept becomes a standalone concept file.

---

## Accepted

- **Schema replacement**: New schema replaces old one for all concepts — no dual schemas
- **New status values**: EXPLORING | READY | BLOCKED (BLOCKED is new at the top level)
- **New complexity values**: SIMPLE | MODERATE | COMPLEX (SIMPLE is new)
- **Blocked section tags**: [CRITICAL] for gaps blocking the concept; [DEFERRED] for gaps acceptable to hand off to the architect
- **Sub-concepts section**: Present only for COMPLEX concepts; omitted for SIMPLE and MODERATE
- **Path location**: `docs/concepts/` relative to each project's repository root
- **Decomposition trigger**: Automatic on COMPLEX assessment AND user-triggered; both are valid entry points
- **Sub-concepts are mutable**: Forge revises sub-concept sections as the concept evolves — no lock-in at first decomposition
- **Sub-concept precision**: Sub-concept definitions must be detailed enough to stand alone in a separate forge session
- **Sub-concept promotion**: The user decides whether a sub-concept becomes its own concept file — forge does not auto-create child files

---

## Blocked

*(none)*

---

## Discarded

- **Home-directory path** (`~/docs/concepts`) — path is repo-relative, not home-dir absolute
- **Separate file per sub-concept** — sub-concepts are sections in the parent file; promotion to standalone files is a user decision
- **Dual-schema approach** — one schema for top-level concepts, another for sub-concepts was ruled out; new schema is unified

---

## Open Questions

1. ~~**OQ1: Schema scope**~~ — **RESOLVED.** New schema replaces old one for all concepts.
2. ~~**OQ2: Path location**~~ — **RESOLVED.** `docs/concepts/` relative to each project's repository root.
3. ~~**OQ3: Decomposition trigger**~~ — **RESOLVED.** Both automatic (COMPLEX assessment) and user-triggered; sub-concepts are revisable throughout the session.
4. ~~**OQ4: Sub-concept storage**~~ — **RESOLVED.** Sections within the parent file; user decides if any become standalone concept files.

---

## Ready for Architecture

**Concept summary**: Update the forge skill in two ways. (1) Replace every occurrence of `docs/concept/` with `docs/concepts/` (repo-relative) in the startup sequence, process steps, and document format examples. (2) Replace the current concept document schema with the new unified format: status values are EXPLORING | READY | BLOCKED; complexity values are SIMPLE | MODERATE | COMPLEX; the Blocked section uses [CRITICAL] and [DEFERRED] tags; COMPLEX concepts include a Sub-concepts section where forge decomposes the concept into named sub-concepts (each with status and notes), triggered automatically on COMPLEX assessment or on user request. Sub-concepts are sections in the parent file, are mutable throughout the session, and are written precisely enough to seed a standalone forge session. The user decides when and whether a sub-concept becomes its own file.

**Key constraints**:
- `docs/concepts/` is repo-relative — must hold for all path references in the skill
- New schema is the only schema — no parallel format for sub-concepts
- Sub-concepts never auto-create separate files
- Sub-concept decomposition is revisable at any point in the session

**Confirmed directions**:
- Unified schema with BLOCKED status, SIMPLE complexity, [CRITICAL]/[DEFERRED] Blocked tags
- Sub-concepts as sections within the parent concept file
- Decomposition triggered by COMPLEX assessment or explicit user request

**Discarded alternatives**:
- Home-directory path (`~/docs/concepts`) — repo-relative confirmed
- Separate files per sub-concept — user-promoted only
- Dual schemas (one for top-level, one for sub-concepts) — rejected in favor of one unified schema

**Blocked (deferred)**:
*(none)*

**Open questions for the architect**:
- None — concept is fully specified
