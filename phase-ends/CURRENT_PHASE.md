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
- [ ] §8 — Path A: Mode 1 intake (from `decomp-architect/intake.decomp.md`) → Gate 1 → Gate 2 → generation; placeholder audit
- [ ] §9 — close the install phase (PhaseEnd, archive, commit, hard stop)

## Current task

**NOW:** §8 — Mode 1 intake done; Gate 1 review presented, awaiting the developer's adjustments
**NEXT:** §8 — Gate 2, then generation
**Last rules check:** n/a (installer)

## Per-task checkpoint log

- **§1** — Path A (new project) detected: the repository is empty except the two package folders. The developer chose, before the install, a new project: THUG2 Remix (PSP) decompilation, governed by ProjectArchitect 2.0.0 recovered from the ProjectArchitect repository's history (commit `56effae`, the last tree carrying `project-architect-2.0/`; upstream `main` now ships 3.x, which the decomp kit refuses). Verified: `git rev-parse --show-toplevel` = repository root.
- **§2** — Phase files bootstrapped from the package templates. Verified: `phase-ends/README.md`, both templates, `logs/.gitkeep` and this file exist.
- **§3** — Path A layout created (`docs tools .run .claude-state/memory .claude-state/transcripts`). Verified: directories exist.
- **§4** — Methodology copied to `docs/project-architect.md`; effort map, cookbook (named `docs/matching-cookbook.md` for the project's recurring craft), ops-setup and registry copied verbatim with copy-time placeholders filled by exact token substitution; backup script installed; PA's ignore block appended. Verified: `grep -c "{{PROJECT_NAME}}"` = 0 in the registry and the effort map; `git check-ignore .run` succeeds; the remaining `{{…}}` are generation-time (§8).
- **§5** — `CLAUDE.md` copied and its copy-time placeholders filled; `.claude/settings.json` (SessionEnd hook) and the machine-local `.claude/settings.local.json` written; 16 memory seeds copied. Dev interview (2026-10-11): LunkezB, solo, BEGINNER (a university assembly course, mostly forgotten; new to decompilation and matching), motivation = the Remix build's content absent from PC THUG2 plus learning PSP decompilation to reuse on other PSP games; accepted defaults: autonomous within phases, recommendation-first options, breadth fan-out welcome, repository text in English. Verified: 16 seeds; both settings files parse; `autoMemoryDirectory` absolute, ends in `/.claude-state/memory`; no `INSTALL INTERVIEW` comment left in `who-is-dev.md`.
- **§6** — SKIPPED by environment: `~/.claude` here is the ephemeral claude.ai cloud harness's own config (launcher settings, session hooks), not the developer's machine; writing a statusline or merging user settings into it would alter the harness and vanish with the container. When the developer runs the project in local Claude Code, run §6 there once (statusline + user-settings merge, skip-if-present). Verified: `~/.claude/statusline.sh` absent, nothing written under `~`.
- **§7** — Checkpoint commit by explicit path, trailer-free (P/H6 and the installer's §0.6; the project's memory rule `no-commit-co-author` governs over the harness's default trailer). Git identity: `LunkezB <181133849+LunkezB@users.noreply.github.com>` (the developer's GitHub noreply address, chosen for a public repository).

## Blockers / open questions

- none

## Notes / deviations

- **Harness:** this install runs in a claude.ai cloud workspace (Claude Code tooling, no `/effort` toggle, no session restart between installers). §6 writes under `~/.claude`, which here belongs to the ephemeral cloud harness, not the developer's machine — see §6's entry.
