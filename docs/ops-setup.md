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

## Decomp environment (decomp-architect, Phase 0.5 — installed 2026-10-11)

### Version pins (decomp)

| Component | Version | Notes / why pinned |
|---|---|---|
| The pinned toolchain triple (compiler → assembler shim → binutils, with flags) | TODO(phase-4) | TODO(phase-4): pinned by fingerprint evidence down the candidate ladder; the assembler's compatibility version is always passed explicitly — a shim's default is not "latest" |
| Candidate compiler family (from the SDK evidence) | the PSP compilers of 2004-05: Sony psp-gcc (GCC-based), SN Systems pspsnc, Metrowerks mwccpsp (all three are decomp.me candidates); possibly mixed per module; C and/or C++ | the candidate set the pin phase runs down; never a sibling project's triple |
| The splitter / disassembler and its config | TODO(phase-3) | version pinned in the bootstrap script |
| The disassembler database and its agent server | TODO(phase-2) | the static oracle; the database is tracked as a TEXT export with a rebuild script |
| The emulator and its scripting bridge | TODO(phase-2) | the runtime oracle |

### The game and the medium

- **Title / platform / serial:** Tony Hawk's Underground 2: Remix · PlayStation Portable (PSP) · the Feb 17, 2005 prototype build (serial to be read from the image's PARAM.SFO in Phase 1)
- **The main executable on the medium:** `BOOT.BIN` (its hash is the first per-binary contract, Phase 3)
- **Container layout:** a UMD image (ISO 9660): PSP_GAME/PARAM.SFO; code in PSP_GAME/SYSDIR (BOOT.BIN, the unencrypted executable this build boots from, and EBOOT.BIN); game data in PSP_GAME/USRDIR in the game's own archive formats; any further code modules located in Phase 1
- **SDK / compiler-era evidence:** not yet inspected (no dump read at Phase 0.5); Phases 1-2 read the executable's module info, its import stubs (library names and NIDs) and any toolchain strings
- **The dump (machine-local, never committed):** `/mnt/user-data/uploads` — copied once onto a fast local filesystem under `disks/`
  (ignored); the extractor reads it, nothing builds against it.

### Build / extract / verify (decomp)

```
# extract the medium and verify against the committed manifest
TODO(phase-1)
# the clean fleet verification — every binary from clean → extract → build, exit code read
TODO(phase-3)
```

- **The gate:** a binary is green only when its hash check inside `make build` passes; a match is verified from a CLEAN
  rebuild, never incremental; the executable is gated only by a clean rebuild; a build is verified by its exit code.

### The oracles (decomp)

- **Disassembler MCP:** TODO(phase-2) — verify with one cheap call before any reverse-engineering task; after a
  restart or a program switch, pause and ask the developer to reconnect the client.
- **Emulator bridge:** TODO(phase-2) — a live-memory finding is verified only with three or more consistent datapoints
  or a controlled before/after diff.

### Git posture (decomp)

- **Visibility at day one:** public from the first push (2026-10-11) — the ROM firewall applies either way (`config/firewall.txt`,
  `tools/audit_public.py`, the CI workflow). If ever private, a later flip is gated on the host's object store, never on
  a clean tree.
- Never `git clean -x` in this tree (the game-derived data is ignored-but-present); the backup of the reverse-engineering
  work is the text export + the checksum files + a private archive repository, not the ignored directories.

### Tooling inventory (decomp)

| Tool | Location | Purpose |
|---|---|---|
| `tools/audit_public.py` | `tools/` | the ROM audit (purge paths, the derived hash set, the size cap, the pasted-disassembly check); the first-push gate and the CI job; its sources are `config/firewall.txt` |
| `make format` | `Makefile` | clang-format over `src/` with the tracked `.clang-format` (the community style) |
| TODO(phase-1): the extractor, the manifest | `tools/` | — |

### The three dictionaries (the kit master copy — consulted, never copied into this repository)

| Corpus | Where | How to use it |
|---|---|---|
| The tool dictionary — the source project's tools, verbatim, by ladder phase, keyed by the need each answers | `<kit master copy>/decomp-architect/corpus/tools/INDEX.md` (installed summary: `docs/tools-manifest.md`) | before designing or debugging a tool, grep the index by the need; the matching file is the jumping-off point, its Adapt column the list of what differs here |
| The inherited knowledge base — the cookbook, its symptom index and the codegen map, verbatim | `<kit master copy>/decomp-architect/corpus/cookbook/` (installed front page: `docs/knowledge-corpus.md`) | same compiler family: look the symptom up, apply, re-prove on your bytes; another compiler: read the same pass in your compiler's source and find your own lever |
| The inherited record — the source project's distilled records (the how-to, the decision log, the accelerators, the retrospective, the story, the playbook, the effort doctrine, the readability charter) and every phase-end, verbatim | `<kit master copy>/decomp-architect/corpus/record/` (installed front page: `docs/inherited-record.md`) | when a rule or kernel cites a source, open it here; the digest first, a phase-end on demand, the how-to in order |
| Kit master copy location | `https://github.com/Druthulu/BFM-decomp/tree/e63ef6b54f0ccbbb656f963813585c4d9dce36bc/decomp-architect` (the commit this install used); clone it beside this repository when a corpus file is needed — the cloud workspace keeps no copy between sessions | — |
