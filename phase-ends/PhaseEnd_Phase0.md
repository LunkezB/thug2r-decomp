# PhaseEnd — Phase 0: Governance install & constitution

**Date:** 2026-10-11 · **Project Version:** 0.1.0 · **Phase Status:** Complete

> Written only at a developer-confirmed milestone (Tier-1 task, `/effort max`). This is the durable synthesis a fresh session reads — write it as if `CURRENT_PHASE.md` will never be read again (it is archived to `phase-ends/logs/`, out of the load order). Keep it lean: non-derivable content only (target ≤30 KB).

## Build Log

**Files created/changed and complete — do not recreate:**
- `CLAUDE.md` — the entry point: session-start, mandatory behaviour, fail-safes (with the four decomp fail-safes), reasoning, phase boundary, project constraints, environment — auto-loaded every session; the kit appends its decomp sections at Phase 0.5.
- `PROJECT_CONTEXT.md` — the permanent constitution: vision, assumptions, risks, philosophy, key decisions, pipeline, architecture, the Phase 0–10 roadmap with a Milestone line per phase — never edited from here on (P1).
- `RULES_REGISTRY.md` — ProjectArchitect's seed rules (P/E/H/X/M), §E holding only the one-line pointer for the kit's G1–G67, §E′ memory pointers, §F empty.
- `docs/project-architect.md` — the ProjectArchitect 2.0.0 methodology, kept after the package is deleted.
- `docs/effort-map.md` — the effort doctrine and the Gen1 table (Phases 0/0.5; 1–10 defer to the kit's ladder block).
- `docs/matching-cookbook.md` — the cookbook with its pinned context (toolchain `TODO(phase-4)`, language `TODO(phase-2)`).
- `docs/ops-setup.md` — environment, commands as `TODO(phase-N)` lines, the public-repository backup note, the fresh-machine restore.
- `phase-ends/README.md`, `phase-ends/CURRENT_PHASE.template.md`, `phase-ends/PhaseEnd.template.md`, `phase-ends/logs/` — the phase record's scaffolding; `phase-ends/logs/PhaseLog_0.md` is this phase's archived worklog.
- `tools/backup-claude-state.sh` — the H8 state sweep, run by the SessionEnd hook and at every phase boundary.
- `.claude/settings.json` — the SessionEnd hook; `.claude/settings.local.json` — the machine-local memory path (untracked by design).
- `.claude-state/memory/` — the 16 ProjectArchitect memory seeds, `who-is-dev` filled from the interview.
- `.gitignore` — ProjectArchitect's block (the kit rewrites its `.run/` line at Phase 0.5).

**Tools/packages installed:** None (ProjectArchitect 2.0.0 is documents and one shell script).

**Verification results:**
- §4: the project-name placeholder count = 0 in the registry and the effort map; `git check-ignore .run` → ignored.
- §5: 16 memory seeds; both settings files parse as JSON; `autoMemoryDirectory` = `/home/claude/thug2r-decomp/.claude-state/memory`; no interview comment left in `who-is-dev.md`.
- §7: install commit `e56b257`, trailer-free.
- §8: the placeholder audit lists only `docs/project-architect.md` (plus the two phase templates when present); `grep -c "Milestone:" PROJECT_CONTEXT.md` = 11; `grep -c "Governance and the firewall" PROJECT_CONTEXT.md` = 1; generation commit `541b8d2`; the developer confirmed the generated constitution ("ок", 2026-10-11 22:47).
- GitHub: `LunkezB/thug2r-decomp` is public, the session has `push: true`, a dry-run push was accepted; nothing has been pushed.

**Milestone achieved:** SETUP §9's verify — the constitution exists with every skeleton section and a Milestone line for each of Phases 0–10, registry §E carries the kit pointer, the placeholder audit is clean, and the developer confirmed the constitution.

**Next:** Phase 0.5 — decomp-architect: the decomp overlay. Start with the kit's SETUP Step 1 (the version pin and the prerequisites).

## Deviations

| Item | Plan | Actual | Reason |
|---|---|---|---|
| ProjectArchitect version | the current release | 2.0.0, recovered from the ProjectArchitect repository's history (commit `56effae`) | the decomp kit overlays 2.0 exactly; upstream `main` ships 3.x |
| SETUP §6 (statusline, user settings) | install under `~/.claude` | skipped | in the claude.ai cloud workspace `~/.claude` is the ephemeral harness's own configuration; run §6 once on the developer's machine when working locally |
| Gate 2 effort toggle | prompt for `/effort max` and wait | not possible; generation ran in-session | the claude.ai harness has no `/effort` toggle (recorded in `CLAUDE.md` → Environment) |
| Install commits | two (§7, §9) | three: §7, a §8 generation commit, §9 | the generation was committed before the developer's review so the tree stayed clean between turns |
| Phase ladder size | a beginner merges rungs 1–3 and 5–6 | canonical rungs 0–10 kept | the kit's rules and `TODO(phase-N)` markers cite rung numbers; the beginner adaptation is small tasks and plain explanations |
| Hard stop and fresh session | stop here; the next phase in a fresh Claude Code session | the developer directed continuing into Phase 0.5 in the same conversation | the harness has no session restart; seeded memories and hooks take effect the next time the repository is opened in Claude Code |
| `.claude-state/` | committed while private, excluded from a public mirror | memory committed in a public repository; transcripts never tracked | the developer chose a public repository; the kit's firewall ignores transcripts, and they are excluded locally until it lands |

## Commit Message

```
feat: Project Architect 2.0 installed — constitution generated

- ProjectArchitect 2.0.0 governance (Path A) for the THUG2 Remix PSP decompilation
- PROJECT_CONTEXT.md from the decomp-architect intake: Phases 0–10, PSP adaptations, risks
- CLAUDE.md, effort map, cookbook and ops-setup generation-time sections filled
- PhaseEnd_Phase0.md; the install worklog archived
```
*(No `Co-Authored-By` / AI-attribution trailer — H5.)*

## Rules Added This Phase

| Rule | Reason |
|---|---|

*None — the decomp rules arrive as the kit's G1–G67 at Phase 0.5; the harness deviations went into `CLAUDE.md` → Environment and the Deviations table above.*

## PhaseEnd Changelog

`v0.0.0 → v0.1.0` — governance installed; constitution generated and confirmed; no rules added.

## Plain-English Recap

This phase set up the project's "rulebook" before any work on the game itself. ProjectArchitect is a set of documents that
tells the AI how to run a long project: a permanent plan (the constitution, `PROJECT_CONTEXT.md`), a list of rules it re-reads
every session, and a diary of finished phases like this one. The plan for this game was generated from the decomp kit's
questionnaire and your answers: eleven phases, from unpacking the UMD image to the last function rewritten in source, each
ending with a check a machine can verify. Nothing from the game has touched the repository, and nothing has been pushed yet —
that waits for the next phase, which installs the firewall that keeps game files out of git.
