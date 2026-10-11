# CURRENT_PHASE — Phase 0: Governance install & constitution

> The in-flight phase working file: the approved plan, the per-task checkpoint log, and blockers. **Copied from this template at Phase Start** (so the template is never overwritten); updated after every task; it is the crash/compaction recovery point and is in the Session Start load order. At phase close it is absorbed into `PhaseEnd_Phase[N].md` and `git mv`'d to `phase-ends/logs/PhaseLog_[N].md` (outside the load order). **Work accumulates commit-by-commit** — each task commits its changes together with its checkpoint entry here (P4), so this file never lags the code, and any task boundary is a clean handoff to a fresh session.

- **Started:** 2026-10-11
- **Effort baseline:** installer run (SETUP.md §1–§9, Path A) — no per-task effort toggles in this harness (claude.ai cloud session)
- **Context budget:** single session
- **Plan approved:** 2026-10-11 — the plan is exactly "execute SETUP.md §1–§9 in order" (§0.2)
- **Baseline state:** empty git repository holding only the two packages (`project-architect-2.0/`, `decomp-architect/`)

## Milestone (the phase's machine-checkable gate)

SETUP.md §9's verify passes: `PROJECT_CONTEXT.md` exists with every skeleton section and a Milestone line per phase; registry §E holds the one-line kit pointer (intake Part D); the placeholder audit is clean; `phase-ends/PhaseEnd_Phase0.md` exists; both installer commits present and trailer-free.

## Task checklist

- [x] §3 — layout (Path A: `docs tools .run .claude-state/memory .claude-state/transcripts`)
- [x] §4 — docs layer, registry, tools, gitignore
- [x] §5 — CLAUDE.md, agent-state wiring, memory seeding, dev interview
- [x] §6 — global assets (statusline + user settings) — SKIPPED in this harness, see the log
- [x] §7 — install checkpoint commit
- [x] §8 — Path A: Mode 1 intake (from `decomp-architect/intake.decomp.md`) → Gate 1 → Gate 2 → generation; placeholder audit
- [x] §9 — close the install phase (PhaseEnd, archive, commit, hard stop)

## Current task

**NOW:** phase closed
**NEXT:** Phase 0.5 — the decomp-architect kit's SETUP Step 1
**Last rules check:** n/a (installer)

## Per-task checkpoint log

- **§1** — Path A (new project) detected: the repository is empty except the two package folders. The developer chose, before the install, a new project: THUG2 Remix (PSP) decompilation, governed by ProjectArchitect 2.0.0 recovered from the ProjectArchitect repository's history (commit `56effae`, the last tree carrying `project-architect-2.0/`; upstream `main` now ships 3.x, which the decomp kit refuses). Verified: `git rev-parse --show-toplevel` = repository root.
- **§2** — Phase files bootstrapped from the package templates. Verified: `phase-ends/README.md`, both templates, `logs/.gitkeep` and this file exist.
- **§3** — Path A layout created (`docs tools .run .claude-state/memory .claude-state/transcripts`). Verified: directories exist.
- **§4** — Methodology copied to `docs/project-architect.md`; effort map, cookbook (named `docs/matching-cookbook.md` for the project's recurring craft), ops-setup and registry copied verbatim with copy-time placeholders filled by exact token substitution; backup script installed; PA's ignore block appended. Verified: the project-name placeholder count is 0 in the registry and the effort map; `git check-ignore .run` succeeds; the remaining placeholders are generation-time (§8).
- **§5** — `CLAUDE.md` copied and its copy-time placeholders filled; `.claude/settings.json` (SessionEnd hook) and the machine-local `.claude/settings.local.json` written; 16 memory seeds copied. Dev interview (2026-10-11): LunkezB, solo, BEGINNER (a university assembly course, mostly forgotten; new to decompilation and matching), motivation = the Remix build's content absent from PC THUG2 plus learning PSP decompilation to reuse on other PSP games; accepted defaults: autonomous within phases, recommendation-first options, breadth fan-out welcome, repository text in English. Verified: 16 seeds; both settings files parse; `autoMemoryDirectory` absolute, ends in `/.claude-state/memory`; no `INSTALL INTERVIEW` comment left in `who-is-dev.md`.
- **§6** — SKIPPED by environment: `~/.claude` here is the ephemeral claude.ai cloud harness's own config (launcher settings, session hooks), not the developer's machine; writing a statusline or merging user settings into it would alter the harness and vanish with the container. When the developer runs the project in local Claude Code, run §6 there once (statusline + user-settings merge, skip-if-present). Verified: `~/.claude/statusline.sh` absent, nothing written under `~`.
- **§7** — Checkpoint commit by explicit path, trailer-free (P/H6 and the installer's §0.6; the project's memory rule `no-commit-co-author` governs over the harness's default trailer). Git identity: `LunkezB <181133849+LunkezB@users.noreply.github.com>` (the developer's GitHub noreply address, chosen for a public repository).
- **§8 (intake + Gate 1)** — Mode 1 ran from the kit's `intake.decomp.md` (Part A pre-answers kept; the FILL items answered by the developer): motivation = the Remix build's content that the PC Underground 2 lacks (new levels, characters, cutscenes — the developer corrected an earlier reading of "cut content") plus PSP-decomp practice to reuse on other games; developer = beginner, solo; worries = none yet; deployment = claude.ai cloud workspace + public GitHub, local Claude Code as an equal home; resources = 2 cores / 7 GB RAM / ~30 GB free in the workspace. Gate 1 presented the ladder (kept canonical 0–10 instead of the beginner merge, because the kit's rules and `TODO(phase-N)` markers cite rung numbers), the PSP adaptations, the C++ and repaired-image risks; the developer's only adjustment was the motivation wording. The developer also granted the Claude GitHub App write access (verified: `push: true` on the repository; dry-run push accepted).
- **§8 (Gate 2 + generation)** — Gate 2's effort toggle does not exist in this harness; generation ran in-session at the highest reasoning available, recorded as a harness deviation. Generated: `PROJECT_CONTEXT.md` on the skeleton (every section; Phases 0–10 with a Milestone line each; Phase 0 named "Governance and the firewall" for the kit's Step 1.3 check); registry §E left as the one-line kit pointer (intake Part D — no `### G` heading, so the kit installs G1–G67 without an offset); `CLAUDE.md`'s four generation-time sections (the four decomp fail-safes of Part D); the effort map's Gen1 table (Phases 0/0.5 here, 1–10 deferring to the kit's ladder block); the cookbook's pinned context (toolchain and language as `TODO(phase-4)` / `TODO(phase-2)`); ops-setup's commands as `TODO(phase-N)` lines plus the public-repository backup note. The ProjectArchitect corpus was consulted: per intake Part D, no corpus rule is installed before the kit's block; non-decomp kernels go after it at Phase 0.5 or later. Verified: no placeholder outside `docs/project-architect.md` and the two phase templates; `grep -c "Milestone:" PROJECT_CONTEXT.md` = 11.

- **§8 (Gate 2 output review)** — the developer confirmed the generated constitution ("ок", 2026-10-11 22:47).
- **§9** — `PhaseEnd_Phase0.md` written (Build Log, Deviations, Plain-English Recap); `tools/backup-claude-state.sh` swept one transcript into `.claude-state/transcripts/`, which is never tracked (public repository — excluded locally until the kit's ignore block lands); this file archived to `phase-ends/logs/PhaseLog_0.md`. The developer directed continuing into Phase 0.5 in the same conversation (no session restart exists in this harness).

## Blockers / open questions

- none

## Notes / deviations

- **Harness:** this install runs in a claude.ai cloud workspace (Claude Code tooling, no `/effort` toggle, no session restart between installers). §6 writes under `~/.claude`, which here belongs to the ephemeral cloud harness, not the developer's machine — see §6's entry.
