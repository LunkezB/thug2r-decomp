# Ops & Setup — THUG2 Remix decomp

> **Evolvable reference (docs/ layer). Last revised 2026-10-11.** The single document a fresh session — or a fresh machine after an OS reinstall — rebuilds the working environment from. **Keep it current in the SAME change as any tooling/env/hook/path change** (registry H7); it rots silently otherwise. Mark not-yet-verified items `# TODO:` and fill them the next time you run the command.

## Version pins

| Component | Version | Notes / why pinned |
|---|---|---|
| Language/runtime | Python 3.13 (cloud workspace at generation) | the project's own tools; any Python 3.10+ is expected to work — TODO(phase-1): pin when the first tool lands |
| Build tool | | |
| Test runner | | |
| Key dependencies | | |
| clang-format | the system package (cloud workspace) | `make format`, installed at Phase 0.5 — TODO(phase-3): pin the version with the first C/C++ file |

## Environment

- **OS / shell:** Linux (claude.ai cloud workspace), bash; equally Linux/WSL/macOS with local Claude Code
- **Project root:** `/home/claude/thug2r-decomp` in the cloud workspace; any fast local path on the developer's machine
- **Machine notes:** [cores/RAM if it affects concurrency; CI or no-CI; reinstall cadence — anything that shapes ops decisions]

## Build / run / test

```
# build
TODO(phase-3): make build   # the all-assembly baseline with the hash check inside
# run
TODO(phase-2): the runtime oracle — PPSSPP booting the prototype from the dump, with its scripting interface
# test gate (the machine-checkable milestone gate — registry M1/P9)
python3 tools/audit_public.py   # the ROM firewall (Phase 0.5) — exit 0 on the tracked tree
TODO(phase-3): the clean fleet check — every binary from clean → extract → build, exit code read
```

- **The gate:** [what "green" means — modes if any (fast smoke vs full), the pinned known-failures baseline if the suite has pre-existing reds, when the slow suite is required].

## Claude Code integration (this project's agent wiring)

- **Statusline:** `~/.claude/statusline.sh` (model · effort · context · rate limits) — global; re-copy from the package on a fresh machine.
- **Effort baseline:** `effortLevel: "xhigh"` in `~/.claude/settings.json` (Max/Ultracode are session-only — see `docs/effort-map.md`).
- **Agent state (H8):** memory at `.claude-state/memory/` via `autoMemoryDirectory` in **`.claude/settings.local.json`** — *this is an absolute path and is machine-local; on a fresh machine, re-point it at `<this repo's absolute path>/.claude-state/memory`.* Transcripts: the `SessionEnd` hook in `.claude/settings.json` copies them into `.claude-state/transcripts/`; `tools/backup-claude-state.sh` sweeps stragglers (run at every phase boundary).
- **MCP / hooks:** TODO(phase-2): the disassembler's MCP server (template `config/mcp.json.template`, activated at Phase 2); the SessionEnd state hook in `.claude/settings.json` *(any project MCP servers, session hooks, and their lifecycle — e.g. a service a SessionStart hook boots.)*

## Tooling inventory

| Tool | Location | Purpose |
|---|---|---|
| `tools/backup-claude-state.sh` | `tools/` | sweep agent state → `.claude-state/` (H8) |
| `tools/audit_public.py` | `tools/` | the ROM audit — installed at Phase 0.5 |

## Backup & git posture

- Commit cadence: per completed task, after updating `CURRENT_PHASE.md` (P4); the developer pushes (H6); no AI-attribution trailers (H5).
- Generated/regenerable outputs are gitignored; decision records are committed (phase-close gitignore discipline).
- `.claude-state/` is committed while the repo is private; **excluded from any public mirror** (transcripts capture full tool output).
- **This repository is public from its first push** (the developer's decision, 2026-10-11): `.claude-state/memory/` (working agreements and the developer profile) is therefore published; transcripts stay ignored by the firewall. The first push happens only after Phase 0.5's audit passes. Commit identity: `LunkezB <181133849+LunkezB@users.noreply.github.com>` (repo-local git config).

## Fresh-machine restore checklist

1. Clone the repo to a fast local filesystem.
2. Install the pinned toolchain (Version pins table above).
3. Copy `project-architect-2.0/statusline/statusline.sh` → `~/.claude/statusline.sh`; merge the settings snippet into `~/.claude/settings.json`.
4. Re-point `.claude/settings.local.json`'s `autoMemoryDirectory` at this clone's absolute `.claude-state/memory` path.
5. Run the test gate to confirm the environment is live.
6. Copy the dump to the new machine (outside the repository) and update the machine-local dump path in the Decomp environment section below; then run `python3 tools/audit_public.py` and, from Phase 3 on, the clean fleet check.
