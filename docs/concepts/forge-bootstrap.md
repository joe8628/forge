# Concept: Forge Bootstrap

**Status**: READY
**Complexity**: MODERATE
**Created**: 2026-04-06
**Updated**: 2026-04-07

## Summary

When forge is invoked, it performs a pre-flight check on `docs/concepts/` (repo-relative) before entering its normal exploration flow. If multiple concept files exist, forge loads all of them as context, infers which is most relevant to the current session, and confirms the selection with the user. If no existing file fits — or if no files exist at all — forge enters bootstrap mode: it asks the user to describe where the project's concept information lives (codemap, architecture file, spec, or other sources), uses that input to generate an initial concept file in forge document format with `Status: EXPLORING`, suggests a filename derived from the inferred concept name, and asks the user to validate the name before writing the file to `docs/concepts/[validated-name].md`.

Once a concept file is active (selected or newly created), forge enters its standard iterative validation loop — identical to a new concept session. Output quality reflects user input: a user who points to rich sources produces a detailed concept file; one who doesn't know the code produces a lighter, inference-based starting point. When the session reaches READY, forge appends the "Ready for Architecture" section and updates Status to READY.

## Accepted

- **Pre-flight check**: Forge checks `docs/concepts/` (repo-relative) as its first act when invoked
- **Multi-file context**: All existing concept files are loaded as context for the session
- **Inference-then-confirm selection**: Forge infers the most relevant file and confirms with the user before proceeding; user can override
- **Bootstrap trigger**: Activates when no files exist OR when inference determines no existing file fits the current concept
- **User-guided sourcing**: During bootstrap, forge asks the user to describe where the concept lives before analyzing; output quality reflects input quality
- **Filename validation**: Forge suggests a filename derived from the inferred concept name; user must confirm or change it before the file is written
- **Initial status**: EXPLORING — written immediately after filename is validated
- **Validation loop**: After writing the EXPLORING file, forge enters the same iterative questioning loop as any new concept session
- **Final write**: On READY, forge appends "Ready for Architecture" and updates Status field
- **Active file scope**: Only the confirmed active file is updated; all other concept files remain read-only context

## Blocked

*(none)*

## Discarded

- **One concept file per repo (fixed path `docs/concepts/concept.md`)** — multiple files supported per repo; a fixed path cannot accommodate multiple concepts
- **Explicit user selection from a list** — replaced by inference-then-confirm; lower friction and handles ambiguity through confirmation rather than enumeration
- **Bootstrap triggers only when zero files exist** — bootstrap also triggers when files exist but none fits the current concept; zero-files is one entry point, not the only one
- **Silent auto-generation without user input** — discarded because user-guided sourcing produces meaningfully higher quality concept files; inference alone fills gaps with noise
- **Separate lighter schema for auto-generated files** — discarded in favor of forge document format throughout; consistency preserves continuity across sessions

## Ready for Architecture

**Concept summary**: Forge gains a pre-flight startup sequence that checks `docs/concepts/` (repo-relative), loads all existing files as context, and infers the most relevant one for the current session (confirming with the user). If no file fits or none exist, forge enters bootstrap mode: asks the user where the concept lives, generates an EXPLORING-status concept file using forge format, validates the filename with the user, then runs its standard validation loop. On READY, the "Ready for Architecture" section is appended and Status updated. Only the active file is modified; all others remain read-only context.

**Key constraints**:
- Pre-flight runs before any other forge behavior
- File is only written after the user validates the suggested filename
- Output quality is intentionally tied to user input quality — no fabrication to fill gaps
- Initial file status is EXPLORING; READY transition appends the final section
- All concept files are loaded as context; only the active one is written

**Confirmed directions**:
- Inference-then-confirm for file selection
- Bootstrap can trigger even when other concept files exist
- Forge document format used throughout — no separate schema for bootstrapped files

**Discarded alternatives**:
- Fixed single concept file path — multiple files needed
- Explicit list selection — inference-then-confirm preferred
- Bootstrap on zero-files only — also triggers when no file fits
- Silent auto-generation — user-guided sourcing required
- Lighter schema for auto-generated files — forge format throughout

**Blocked (deferred)**:
*(none)*

**Open questions for the architect**:
- None — concept is fully specified
