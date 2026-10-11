# THUG2 Remix decomp — Project Context & Roadmap

> **Version:** 1.0.0
> **Generated:** 2026-10-11
> **Generation:** Gen1 | **Tech Stack:** splat (PSP platform) → the era's PSP compiler (pinned by evidence in Phase 4) → Allegrex-capable binutils → whole-binary hash check; Python tooling; a disassembler database with Allegrex support and an agent server (static oracle); PPSSPP (runtime oracle)

---

## For Humans — Quick Guide

This is your project's **permanent constitution** — the vision, decisions, architecture, and roadmap. It is written once and **never edited** (rules and state evolve elsewhere). A fresh Claude Code session auto-loads `CLAUDE.md`, which reads this file first.

**The document system (where everything lives):**
- **This file** — permanent vision/decisions/architecture/roadmap. Never edited.
- **`RULES_REGISTRY.md`** — every rule, full text, recited each session.
- **`phase-ends/`** — the append-only build history (`PhaseEnd_Phase*.md`) + the in-flight `CURRENT_PHASE.md`.
- **`docs/`** — evolvable references (effort map, cookbook, ops-setup, the methodology spec).

**To work on this project:** open Claude Code in the repo and say "continue" — the Session Start Protocol takes over. Governance methodology: `docs/project-architect.md`.

---

## Rules & Protocols

The AI collaboration rules and the Session Start / Phase Start / Phase Boundary protocols are **not** in this file (a permanent-static file would freeze them). They live in:
- **`RULES_REGISTRY.md`** — the canonical, full-text rule set (P/E/H/X/M groups + this project's §E rules + accumulated §F phase rules). Recited every session.
- **`CLAUDE.md`** — the operating protocols (session start, mandatory behavior, phase boundary, reasoning/effort).

**Precedence:** where this permanent file's wording ages out of step with them, `CLAUDE.md` + `RULES_REGISTRY.md` govern; `docs/effort-map.md` governs effort language.

---

## Quick Reference Card

- **Project:** THUG2 Remix decomp — a matching decompilation of *Tony Hawk's Underground 2: Remix* for the PlayStation Portable, the Feb 17, 2005 prototype build.
- **Goal:** every executable on the prototype's UMD image rebuilds byte-identical from C/C++ source, verified by a hash check inside every build — and the methods and tools built on the way transfer to the next PSP decompilation.
- **Definition of done (the milestone gate):** the whole-binary hash of each onboarded executable equals the original's, from a clean rebuild, with the check inside `make build` (registry M1; the kit's byte gate). Nothing else counts as progress.
- **Stack:** splat (PSP) → the era's PSP compiler (candidates: Sony `psp-gcc`, SN Systems `pspsnc`, Metrowerks `mwccpsp`; pinned in Phase 4) → Allegrex-capable binutils → hash check; Python tooling; disassembler database with Allegrex support + agent server; PPSSPP.
- **Environment:** see `docs/ops-setup.md`.
- **Current generation:** Gen1 — the prototype's main executable (`BOOT.BIN`) and any code modules on the same image, from an all-assembly byte-identical baseline to 100% source, published and readable.

---

## Project Overview

*Tony Hawk's Underground 2: Remix* is the PSP version of Neversoft's *Tony Hawk's Underground 2*, adapted for the handheld by
Shaba Games with Neversoft and published by Activision; it was a launch title (North America March 24, 2005; Europe
September 1, 2005). It is not a straight port: it adds levels, characters and cutscenes that the console and PC versions do
not have. This project produces C/C++ source that, compiled with the original era's toolchain and linked in the original
order, reproduces the game's executable byte for byte.

**Why this game.** The Remix build carries content that the PC version of Underground 2 does not, and its code is the only
complete description of how that content works. The project is also deliberate practice in PSP decompilation: the
developer intends to reuse its methods and tooling on other PSP games, so platform-generic machinery (the split, the
Allegrex toolchain, the oracles, the census and the campaign tools) is kept apart from what is specific to this game.

**The target build.** The Feb 17, 2005 prototype — a build dated two days after the US final (Feb 15, 2005) and three
months before the EU final (May 26, 2005), found as filler data on the PS2 disc of *Shrek SuperSlam* and documented by Hidden
Palace. It boots from `BOOT.BIN`. The retail US and EU builds are later, separate targets (stretch, item 7 of the intake).

**Decomp-first, not recompilation-first** (the decision that precedes the first commit): a matching decompilation needs no
recompiler and a recompiler's output feeds no matching work; the memory map comes from the loader's own code and the
runtime oracle. Ports, recompilation and asset tooling are a later generation.

### Generation Map

- **Gen1 — the matching decompilation:** the prototype's main executable (`BOOT.BIN`) and any code modules on the same image, from an all-assembly byte-identical baseline to 100% source, published and readable. *(this roadmap)*
- **Gen2 — more builds, shiftable code:** the US and EU retail executables as additional split configurations sharing the prototype's source; a shiftable build (code that still links when moved); documentation of the Remix-exclusive content from the source. Requires Gen1's readable, symbolic source.
- **Gen3 — derived work:** asset export and repacking, modding hooks, and — only if wanted then — a port or native recompilation. Requires Gen2's shiftable build.

### Project Assumptions

- The developer owns the dump that the project builds against; it lives outside the repository (`/mnt/user-data/uploads/` in the cloud workspace, any absolute path on a local machine) and no byte of it is ever committed.
- `BOOT.BIN` on the prototype image is an unencrypted PSP executable (Hidden Palace notes that the build boots from `BOOT.BIN`); whether it is a static ELF or a relocatable PRX, and whether it carries symbols, is checked in Phase 1.
- The game was built with one of the PSP compilers of its era — Sony's GCC-based `psp-gcc`, SN Systems' `pspsnc` or Metrowerks' `mwccpsp` (all three exist as candidates on decomp.me) — possibly more than one across modules. Which one is a Phase-4 verdict from the bytes, never an assumption.
- Neversoft's engine is most likely C++ (classes, virtual tables, constructors); this is a hypothesis to confirm from the bytes in Phase 2 (virtual-table layout, constructor/destructor shapes, any mangled names). The kit's material assumes C; where C++ differs, the project records its own rules.
- The work runs in a claude.ai cloud workspace (2 cores, 7 GB RAM at generation) with the repository on GitHub; local Claude Code on the developer's machine is an equal home, reached by the fresh-machine restore in `docs/ops-setup.md`.
- The developer is a beginner in decompilation and matching; the agent does nearly all of the work between the two gates of each phase and explains each step in plain words; the developer decides at the gates.

---

## Lessons Learned / Known Risks
*(For a migrated or existing-code project: pre-existing debts, dead-ends already tried, and risks discovered from the codebase go here — document reality, not aspiration. Omit if greenfield with none.)*

Greenfield, so there are no project debts yet. The risks are inherited from the kit's failure museum (`docs/decomp-kernels.md`
after Phase 0.5) and from what is already known about this target:

- **Almost every recorded wall was one of the project's own instruments** (DK-9, DK-17) — the differential harness and the coverage assertions are planned at 0% (Phase 5), not after the numbers look wrong.
- **Integration, not idioms, is the bottleneck once cracking is systematic** (DK-7) — budget for banking.
- **A wrong compiler era or a silent assembler default produces systematic near-misses everywhere** (DK-3) — on the PSP there are three candidate compiler families, and the assembler must know the Allegrex extensions (and VFPU instructions, if the game uses the vector unit) exactly as the original toolchain encoded them.
- **ROM-derived bytes committed "while private" cost a full-history rewrite** (DK-1, DK-53–56) — this repository is public from its first push, which makes the firewall a day-one gate rather than a policy.
- **Model-drafted outward text costs goodwill** (DK-58); **names guessed by a model damage a decompilation without any test catching it** (G62).
- **Structural decisions get more expensive as matched work accumulates** (DK-12) — segment at the forced boundaries before any source exists.
- **A fresh session misreads a compressed hand-off** (DK-59) — the checkpoint is replayed, never summarised.
- **The engine is probably C++.** Matching C++ adds virtual tables, constructors and destructors, inlined member functions, templates and exception/RTTI data to everything the kit's PS1-era material describes; the kit's cookbook levers do not transfer, only its entry structure (G67).
- **The prototype image was repaired.** Hidden Palace reports that the original file was truncated after its first 885 MB and that the missing sectors were filled from the neighbouring builds; every file on the image — `BOOT.BIN` first — must be checked against the image's own directory records before it is trusted as this build's bytes.
- **The kit was written for the PlayStation / PsyQ generation.** Its `TODO(platform)` markers name each place where the PSP needs its own answer: the disassembler loader, the runtime oracle, the SDK signatures, the compiler family.
- **The cloud workspace is small** (2 cores, 7 GB RAM at generation); a permuter and large fan-outs are CPU-bound. Phase 2 measures whether the oracles run here; the fallback is the developer's own machine.
- **Scale and a beginner developer.** A full commercial C++ game is thousands of functions; a realistic horizon is months. Phases are kept small inside, every step is explained, and progress is only ever reported from the byte gate.

---

## Project Philosophy

**North Star (one sentence):** The bytes decide — a function is done when the rebuilt executable's hash says so, and not one moment before.

- **Tooling before campaign.** The order of work is the kit's ladder: extraction, oracles, an all-assembly baseline and the pinned compiler come before the first real match; the census, the harness, the multipliers and the codegen map come before the campaign. Phases 5–7 end in running tools, never in plans.
- **Evidence over assertion.** Every address, name, type and compiler claim carries its evidence (a string, a cross-reference chain, a live-memory datapoint, a byte proof). Unnamed beats wrong.
- **Nothing from the game in git.** The firewall is in force from the first commit; the repository ships tools, configuration, documentation and source only.
- **Readable from the first bank.** The six inversions (intake Part C) apply at draft time: pins recorded, shared bodies as files per system, canonical types with no raw address casts, names with evidence, formatting installed, file layout from the game's systems.
- **Transferable by construction.** Anything that is about the PSP rather than about THUG2 — the split conventions, the Allegrex toolchain wiring, the oracle bridges, the census — is written so the next PSP project can lift it.
- **Explain, then act.** The developer is learning; each phase's plan and each checkpoint say in plain words what was done and what it means.

---

## Key Decisions

| Decision | Choice | Rejected alternative | Why |
|---|---|---|---|
| Order of work | Decomp-first: a matching decompilation from the shipped bytes | Recompilation-first | A recompiler's output feeds no matching work; the memory map comes from the loader's code and the runtime oracle (the kit's failure museum, first exhibit) |
| Target build | The Feb 17, 2005 prototype's `BOOT.BIN` | The US retail build first | It is the developer's dump; retail US and EU follow as extra split configs sharing the source (Gen2) |
| Governance | ProjectArchitect 2.0.0 (recovered from its repository's history, commit `56effae`) + the decomp-architect kit as Phase 0.5 | ProjectArchitect 3.x (upstream `main`) | The kit overlays version 2.0 exactly and refuses any other; its phase ladder, rules and firewall are the point |
| Phase numbering | The kit's canonical ladder, Phases 0–10, kept as numbered | Merging Phases 1–3 and 5–6 (the kit's suggestion for a beginner) | The kit's rules and its `TODO(phase-N)` markers cite rung numbers; the beginner adaptation is small tasks and plain explanations inside each phase instead |
| Visibility | Public from the first push; the first push happens only after Phase 0.5 | Private until a later flip | The developer's choice; the firewall applies either way, so the audit and the CI must exist before anything leaves the machine |
| Compiler | Not chosen: pinned by fingerprint evidence in Phase 4 from the candidates `psp-gcc`, `pspsnc`, `mwccpsp` | Adopting a sibling project's triple | A wrong era or default yields systematic near-misses everywhere (DK-3) |
| Where the work runs | claude.ai cloud workspace + GitHub, with local Claude Code as an equal home | Local only | The developer started here; the repository is the hand-off, and Phase 2 measures whether the heavy oracles run in the cloud |
| Licensing | The project's own tools and documentation under the MIT license; no license is asserted over the decompiled source | AGPL-3.0 (the kit's source project) | The developer's choice; the decompiled source describes a work the project does not own |
| Repository language | English for documents, code and commits; the developer and the agent converse in Russian | Russian documents | The decompilation community's standard; contributors and tools expect English |
| Platform-generic vs game-specific | PSP machinery kept separate from THUG2 configuration and knowledge | One undifferentiated tree | The developer's second goal is reuse on the next PSP game |

---

## Core Logic / Strategy

The pipeline every matching decompilation of this generation runs, with the PSP's answers filled in where they are known:

1. **Extract.** The project's own deterministic extractor reads the developer's UMD image (ISO 9660), writes every file under
   `extracted/` (ignored) and a committed manifest of hashes; a second run reproduces the manifest; sampled payloads agree with
   a reference extractor. Game archives inside `PSP_GAME/USRDIR` are unpacked to their decompressed payloads, which are what
   the manifest verifies.
2. **Map.** The static oracle (a disassembler database with Allegrex support, exported to tracked text with a proven rebuild)
   and the runtime oracle (PPSSPP, scripted) establish where code loads and where the forced boundaries are: jump-table spans,
   optimisation-level changes, library objects, module boundaries.
3. **Split.** splat, driven by a per-binary configuration and a curated symbol file, emits per-function assembly and a linker
   script; translation-unit boundaries sit at the forced boundaries.
4. **Build.** A modern preprocessor → the pinned compiler → the assembler behaviour of the era → binutils for assemble, link
   and objcopy → the whole-binary hash check inside `make build`. At first, every function is assembly and the build is
   byte-identical; from then on each function is swapped from assembly to source only when the hash stays equal.
5. **Match.** Per function: decompile a draft, compile, diff against the original, apply levers from the cookbook, run the
   permuter for the residue, and bank only through the byte gate. Matches propagate to identical and near-identical
   functions across the fleet; every function is on a ledger with a class, a closeness and a named blocker.
6. **Learn.** Every reusable lesson goes into the cookbook (symptom-keyed) and, where mechanical, into a tool — the flywheel.

### Component Inventory

| Component | What it is | Built in |
|---|---|---|
| The firewall | `config/firewall.txt`, `tools/audit_public.py` (with its planted negative control), the no-ROM CI workflow, the ignore block | Phase 0.5 |
| The extractor + manifest | deterministic UMD and archive extraction, the committed hash manifest, format notes | Phase 1 |
| The static oracle | the disassembler database with Allegrex support, its agent server, the text export and rebuild script | Phase 2 |
| The runtime oracle | PPSSPP with a scriptable memory/debug interface; the load-map tool | Phase 2 |
| The build | the Makefile pipeline, the per-binary contracts (hashes), splat configs, the boundary check | Phase 3 |
| The pinned toolchain | the compiler triple with flags and its fingerprint evidence; the probe and differ wrappers | Phase 4 |
| The census + harness | coverage-asserting scanners, a second oracle, the differential harness, the progress report from the build | Phase 5 |
| The multipliers | signatures, dedup propagation, families, the reconcile ladder, the carve chain, the draw filter, the canonical type layer | Phase 6 |
| The codegen map + permuter | compiler-source citations per pass, the reproducer battery, the permuter with a masked scorer, the plateau classifier | Phase 7 |
| The campaign machinery | cards, packs, lanes, waves, gates in worktrees, the harvest and recovery tools | Phase 8 |
| The publication | the contract run, the bootstrap script, generated numbers, the README path from a fresh clone | Phase 9 |

---

## Safety / Guardrails / Error Handling

- **The ROM firewall, from the first commit, with no private exemption** (G12–G18, DK-1). The dump, extracted payloads,
  generated assembly, assets, build output, memory images, the disassembler database, the vendor SDK, transcripts that quote
  disassembly and any text that pastes the target's instructions never enter git. `tools/audit_public.py` (proven to fail
  on a planted file before it is trusted to pass) runs before every push and in CI on every push.
- **The byte gate is the only definition of done** (G3, G61; M1). No unmatched source in a default build (G4); a match is
  verified from a clean rebuild, never an incremental one; a build is verified by its exit code.
- **The AI-conduct rules** (G61–G65): the byte gate is the only claim of success; names and types only with evidence (a
  model proposes, a person with evidence asserts); outward text to third parties is written by a person; no automated
  traffic against community infrastructure; every change is justifiable by a person from the record.
- **Never `git clean -x`** in this tree — the game-derived data is ignored-but-present, and a `-x` clean deletes the
  disassembler database. `make clean` is the only clean.
- **The dump stays outside the repository** and is only read; nothing builds against it directly.
- **Scratch lives under `.run/`** (ignored, with dated tracked exceptions), never in system temp (H4).
- **Git:** commits per task by explicit path, no AI-attribution trailers; the agent pushes only when the developer has
  directed it, and never before the audit passes.

---

## Architecture

### Project Structure

```
thug2r-decomp/
├── CLAUDE.md                 entry point: protocols, fail-safes (auto-loaded)
├── PROJECT_CONTEXT.md        this constitution (never edited)
├── RULES_REGISTRY.md         every rule, full text (P/E/H/X/M, §E G1–G67 from Phase 0.5, §F per phase)
├── phase-ends/               PhaseEnd_Phase*.md, CURRENT_PHASE.md, DIGEST.md, logs/ (archived worklogs)
├── docs/                     methodology, effort map, cookbook, ops-setup, kernels, tools manifest, format notes
├── config/                   firewall config, splat configs, symbol files, per-binary contracts   (tracked)
├── tools/                    the project's own tools (audit, extractor, build helpers, oracles' bridges)
├── src/                      matched source, laid out by the game's systems; NOTICE.md
├── include/                  shared headers; the canonical type layer
├── .github/workflows/        the no-ROM CI
├── .claude/ .claude-state/   agent settings and memory (memory tracked; transcripts ignored)
├── .run/                     scratch (ignored; README and dated exceptions tracked)
├── disks/                    the developer's dump, copied locally          (ignored)
├── extracted/                extracted payloads; extracted/retail/manifest.jsonl is tracked
├── asm/  build/              generated assembly and build output           (ignored)
└── dumps/  ghidra/           memory images, the database                   (ignored)
```

### Services / Dependency Wiring

- **The static oracle** — a disassembler database with Allegrex support (a candidate is Ghidra with the `ghidra-allegrex`
  extension), served to the agent through an MCP server; wired in Phase 2; config template `config/mcp.json.template`.
- **The runtime oracle** — PPSSPP with a scriptable debugging/memory interface; wired in Phase 2.
- **The compiler** — run through a wrapper (natively or under a Windows-binary shim, depending on which candidate wins);
  pinned in Phase 4.
- **CI** — GitHub Actions runs the ROM audit (and, from Phase 4, a compile of every translation unit with the pinned
  toolchain); byte identity is verified where the dump is, and recorded.
- No other services. Every new tool is justified (what it does / existing overlap / the specific delta) before adoption.

### Config / Settings

- `config/firewall.txt` — the audit's sources: purge paths, required/pending hash sources, the size cap.
- The splat configuration and the curated symbol file per executable, and the per-binary contract (its expected hash) —
  Phase 3 creates them under `config/` and decides their exact names.
- `.claude/settings.json` — the SessionEnd state hook; `.claude/settings.local.json` — machine-local memory path (untracked).
- `docs/ops-setup.md` — every version pin, command and endpoint; updated in the same change as any tooling change (H7).

---

## Testing & Validation Strategy

- **The byte gate** — the whole-binary hash of each executable, inside `make build`, from a clean rebuild. It is the
  project's M1 instance and the only claim of success.
- **The firewall audit** — `tools/audit_public.py` over the tracked tree, plus its negative control (it must fail on a
  planted file); in CI on every push and locally before every push.
- **Determinism checks** — the extraction manifest reproduced by a second run; the disassembler database's text export
  round-tripped through its rebuild.
- **Live-memory claims** — a runtime finding counts only with three or more consistent datapoints or a controlled
  before/after diff (M3).
- **Instrument integrity** (Phase 5 on) — every scanner asserts its own coverage; a second oracle must disagree with the first
  on nothing; the differential harness runs question pairs on a schedule; every percentage is checked against a case whose
  answer is already known.
- **Integration** — the fleet is green from a clean rebuild after every banked batch.

**Pass criteria:** a phase passes only on its Milestone line below, demonstrated by a command's output; the project passes
when every executable on the image is N of N byte-identical from source from a clean rebuild, the census reads zero stubs,
and a stranger with their own dump can extract, build and verify from the README alone.

---

## Build Roadmap

*Each phase produces something runnable and testable, and ends with an observable, machine-checkable **Milestone** (the gate that P9/M1 hold it to). Validation is a dedicated phase; enhancement layers are toggleable and added one at a time.*

*The ladder is the decomp-architect kit's canonical one (intake Part B), adapted to the PSP; each phase's "earned by" kernels are
in `docs/decomp-kernels.md` and its rules in registry §E. Size inside each phase is kept small for a beginner developer.*

### Phase 0 — Governance and the firewall (ProjectArchitect's install + the kit's Phase 0.5)
- [ ] ProjectArchitect 2.0 installed; this constitution generated from the kit's intake
- [ ] The kit installed as Phase 0.5: the firewall pack (ignore block, `config/firewall.txt`, the audit with its planted fixture, the no-ROM CI), the layout READMEs, registry §E G1–G67, the overlays, the memory seed, the skeletons (LICENSE with the MIT text, NOTICE, README, CONTRIBUTING, `.clang-format`, `make format`)
- [ ] First push to the public repository, only after the audit passes
- [ ] **Milestone:** the ROM audit FAILS on the planted fixture and PASSES on the tree; the no-ROM CI workflow is green on the first push; this constitution carries the ladder; the registry holds G1–G67.

### Phase 1 — Deterministic extraction with a committed manifest
- [ ] Read the image's identity: the serial and version from `PARAM.SFO`, the image size, the directory records
- [ ] Integrity check of the repaired image: every file's extent checked against the directory records and the truncation point Hidden Palace reports; `BOOT.BIN` (and `EBOOT.BIN`) confirmed as this build's bytes or flagged
- [ ] First look at `BOOT.BIN`: executable format (static ELF or relocatable PRX), sections, module info, imports — and whether it carries symbols or debug data
- [ ] The extractor: ISO 9660 → `extracted/`, the game's archive formats in `PSP_GAME/USRDIR` decompressed with a length cross-check; format notes in `docs/`
- [ ] The committed manifest of hashes; the audit reads it as a required hash source (G13)
- [ ] A file inventory of the image (names, sizes, kinds) as the starting map for locating the Remix-exclusive content
- [ ] **Milestone:** one command extracts the whole image; a second run reproduces the manifest identically; sampled payloads agree byte-for-byte with a reference extractor; `git status` shows nothing game-derived staged.

### Phase 2 — The oracles and the load map
- [ ] The static oracle: a disassembler database with Allegrex support, the PSP's library/syscall identification (import stubs by NID), the text export and the proven rebuild round-trip; its agent server wired
- [ ] The runtime oracle: PPSSPP scripted (memory reads, breakpoints) — in the cloud workspace if it runs here, otherwise on the developer's machine, recorded either way
- [ ] The load address of `BOOT.BIN` and of every code module byte-proven against a live memory image (three datapoints or a before/after diff)
- [ ] The language verdict: C, C++ or mixed — from virtual tables, constructor/destructor shapes, mangled names, runtime-library objects
- [ ] The forced boundaries recorded for segmentation: jump-table spans, library objects, module edges
- [ ] **Milestone:** the database is imported with the PSP's library identification and the SDK version evidence recorded; the text export rebuilds; the runtime oracle answers a scripted query; every code load address is byte-proven; the load map is regenerated from the bytes with control rows; the forced boundaries are written down for Phase 3.

### Phase 3 — The all-assembly byte-identical baseline
- [ ] The Allegrex-capable assembler and linker pinned and wrapped; splat configured for `BOOT.BIN` (and any modules)
- [ ] The Makefile pipeline with the hash check inside `make build`; the per-binary contracts
- [ ] Translation-unit boundaries at the forced boundaries from Phase 2; the boundary check in the health target
- [ ] **Milestone:** `make build` produces every onboarded executable with a hash equal to the original at 100% assembly, the check inside the build; `make expected` baseline set.

### Phase 4 — The compiler pinned by evidence
- [ ] The fingerprints: prologue/epilogue shapes, scheduling, register allocation, string and constant pooling, runtime-library calls, any toolchain stamps in the binary
- [ ] The candidate ladder run as parallel probes: `psp-gcc`, `pspsnc`, `mwccpsp` (each at its available versions and flag sets)
- [ ] Per-module variation detected (optimisation levels, mixed compilers, C vs C++ units)
- [ ] The decompile scaffold, the differ invocation, the stub/non-matching headers
- [ ] **Milestone:** three to five probe functions byte-identical under exactly one candidate triple; the triple recorded with its fingerprint evidence and the assembler options passed explicitly; per-module variation recorded; the first functions matched end to end through the whole workflow.

### Phase 5 — The honest census and the differential harness, at 0%
- [ ] Coverage-asserting scanners; a second boundary oracle; the differential harness with at least five question pairs on a schedule
- [ ] The census: duplication, structural families, reach × size, the unique tail — each checked against a known-true case
- [ ] The progress, difficulty and duplicate reports with denominators derived from the build; the health chain that runs them
- [ ] **Milestone:** every scanner asserts its coverage; the second oracle disagrees with the first on nothing; the harness reports 0 disagreements; the progress report derives its denominators from the build.

### Phase 6 — The multipliers
- [ ] Signatures (exact, normalised, sequence) and the twin band; dedup propagation with a fail-closed registry; family remaps
- [ ] The reconcile ladder; the carve chain (optimisation level, jump tables); the draw filter
- [ ] The canonical type layer from the first bank — one definition per shape, widths and signedness proven by the bytes, no raw address cast banked (C++: one definition per class layout and virtual table)
- [ ] **Milestone:** one hand-matched function propagates to every member across the fleet, byte-gated per member; the twin band reproduces every exact pair; a standalone match banks into its real translation unit without a redraft; the carves build; the draw filter refuses what cannot bank and counts it; a bank with a duplicate type definition or a raw address cast is refused.

### Phase 7 — The codegen map and the permuter
- [ ] The pinned compiler's source (or, for a closed compiler, a probe battery) read into a codegen map: at least one byte-proven lever per pass group, a symptom-keyed triage table
- [ ] The permuter with a masked scorer, proven to iterate; the plateau classifier
- [ ] The cookbook seeded from the map and from sibling PSP projects, indexed by symptom with its own coverage assertion
- [ ] **Milestone:** the map holds a byte-proven lever per pass group with its triage table; the permuter runs on a stored draft and proves it iterated; the plateau classifier labels a plateau; the cookbook index passes its coverage check.

### Phase 8 — First cracks, the manual wave, the routing cliff — then the campaign
- [ ] A small manual wave to measure the bank rate by instruction count; routing set from it
- [ ] Cards, packs, lanes, waves; gates in worktrees; the harvest gate closing every wave
- [ ] Every remaining function on a named ledger (class, closeness, best draft, named blocker)
- [ ] **Milestone:** every wave closes with the harvest gate; the fleet is green from a clean rebuild after every banked batch; the census reads 0 stubs.

### Phase 9 — Publish
- [ ] The contract run recorded (clean rebuild, every oracle green, N of N)
- [ ] A fresh clone rebuilds from the developer's own dump by the README alone; every published number generated with a freshness check
- [ ] Releases and outreach written by a person
- [ ] **Milestone:** the contract run is recorded; the fresh-clone proof passes; the no-ROM CI is green; every published number is generated.

### Phase 10 — Readability
- [ ] Pins: zero, or each marked as forced with its reason; shared bodies as files per system, never macros
- [ ] Zero raw address casts; one definition per structure/class; every renamed symbol with its recorded basis
- [ ] Formatting clean
- [ ] **Milestone:** 0 unmarked pins; 0 shared bodies as macros; 0 raw address casts; one definition per structure; every rename with a recorded basis; formatting clean; and, unchanged, N of N byte-identical from a clean rebuild.

---

## Enhancement Backlog
*(Toggleable feature-flagged modules to add one at a time, measured before the next — not scheduled into Gen1 phases yet.)*

- **A map of the Remix-exclusive content** — from the Phase-1 inventory and, as source accumulates, from the code that loads it: which levels, characters and cutscenes are PSP-only and where their data and logic live. Added when the developer wants it; it never gates a phase.
- **A public decomp.me preset** for this game's pinned toolchain — requested from the maintainers by a person (G63–G64).
- **The US and EU retail executables** as additional split configurations (the step into Gen2).
- **Standalone PSP tooling** — the Allegrex toolchain wiring, the oracle bridges and the census tools lifted into a reusable package for the developer's next PSP project.
- **A regenerable reverse-engineering database** — a text-export policy complete enough that the database can be rebuilt from tracked text alone.

---

## Future Generations
*(Evolutionary leaps, not version bumps — sketched, not phase-detailed.)*

- **Gen2 — more builds, shiftable code.** The retail builds share the prototype's source through per-build configuration; the build becomes shiftable; the Remix-exclusive content is documented from the source. Starts only when Gen1 is readable (Phase 10) — every item depends on symbolic, legible source.
- **Gen3 — derived work.** Asset export and repacking, modding hooks, and possibly a port or native recompilation. Starts only on a shiftable Gen2 build.

---

## What Success Looks Like

- Every executable on the prototype's image — **N of N** — rebuilds byte-identical from source from a clean rebuild, with the check inside the build.
- Every game-code function is source; what is not (the vendor's linked libraries, any genuine hand-written assembly of the original) is stated, censused and published, never hidden.
- A stranger with their own dump can extract, build and verify from the README alone.
- Every published number is generated by a tool, never typed.
- The PSP machinery built here is reusable on the developer's next PSP decompilation without archaeology.

---

## Feature & Architecture Inventory

| Feature | Phase | State at generation |
|---|---|---|
| Governance (constitution, registry, phase record, memory) | 0 | being installed |
| ROM firewall (audit + negative control + CI) | 0.5 | planned |
| Deterministic extraction + manifest | 1 | planned |
| Static and runtime oracles, load map | 2 | planned |
| All-assembly byte-identical baseline | 3 | planned |
| Pinned compiler triple | 4 | planned |
| Census, differential harness, reports | 5 | planned |
| Propagation, families, reconcile ladder, carves, draw filter, canonical types | 6 | planned |
| Codegen map, permuter, cookbook index | 7 | planned |
| Campaign machinery | 8 | planned |
| Contract run, fresh-clone proof, generated numbers | 9 | planned |
| Readability pass | 10 | planned |

---

## Data Sources / External Dependencies

- **The developer's dump** of the Feb 17, 2005 prototype image — the only source of game bytes; machine-local, never committed.
- **Hidden Palace's page on the prototype** — the build date, the final-build dates, the truncation-and-repair note, the `BOOT.BIN` boot note. Treated as a lead to verify, not as ground truth.
- **decomp.me** — the PSP compiler candidates (`psp-gcc`, `pspsnc`, `mwccpsp` builds) and, later, a place for a public preset (requested by a person). No automated traffic against it (G64).
- **Open PSP documentation** — the homebrew SDK's headers and PPSSPP's sources for module formats, syscall NIDs and the loader's behaviour.
- **The decomp-architect kit's three dictionaries** — the source project's tools, knowledge base and record, kept in the kit master copy (Druthulu/BFM-decomp, `decomp-architect/`), consulted by need; the PS1-era levers do not transfer, their structure does (G67).
- **Prior community work on this game:** no public decompilation of the PSP version was found on 2026-10-11; the prototype is documented by Hidden Palace, and a fan-made "Revision + Re-Dub" ROM hack of the Remix exists.

---

## Libraries / Dependencies

Candidates, each adopted only with its justification (what it does / existing overlap / the specific delta) and pinned in
`docs/ops-setup.md` when adopted:

- **splat** (with its PSP platform) and its disassembler back end — the split (Phase 3).
- **Allegrex-capable binutils** — assemble, link, objcopy; must encode the Allegrex extensions (and VFPU, if used) exactly as the original toolchain did (Phase 3).
- **The pinned compiler** — one of `psp-gcc`, `pspsnc`, `mwccpsp` (Phase 4), run natively or under a Windows-binary shim.
- **A disassembler with Allegrex support** — e.g. Ghidra with the `ghidra-allegrex` extension — and an MCP server for agent access (Phase 2).
- **PPSSPP** — the runtime oracle (Phase 2).
- **A function differ, a MIPS-to-C draft decompiler and a permuter** — the standard matching tools of the community, checked for Allegrex/PSP support before adoption (Phases 4 and 7).
- **Python 3** for the project's own tools; **clang-format** for `make format`.

---

## Parking Lot
*(Dream features, someday/maybe ideas, out-of-scope thoughts — captured so they're not lost, explicitly not committed.)*

- A shiftable build; asset export and repacking; native recompilation or a port; randomizer-grade tooling; a community-trained matching model (the kit's dream list — all after readability).
- Bringing the Remix-exclusive content to other versions of the game.
- Additional prototypes of the Remix, if more surface, as further split configurations.

---

## Notes for Future Phases

- **Phase 1 opens with three cheap reads** that can reshape the plan: the serial from `PARAM.SFO`, the integrity of the repaired image around `BOOT.BIN`, and whether `BOOT.BIN` carries symbols. Symbols would turn Phase 2's naming work and Phase 3's segmentation into reading rather than inference.
- **The language verdict (Phase 2) decides how much of the kit's material is usable as-is.** If the engine is C++, record the C++-specific rules (class layouts, virtual tables, constructors, member-function naming) in §F as they are proven.
- **Where the oracles run** is measured in Phase 2: if PPSSPP or the disassembler cannot run usefully in the cloud workspace, the oracle work moves to the developer's machine, with the findings recorded the same way.
- **The kit's PS1-specific places** are marked `TODO(platform)` in the installed documents; each is resolved by the phase that meets it, and the resolution is recorded in that phase's PhaseEnd.
- **The kit master copy** stays at Druthulu/BFM-decomp (`decomp-architect/`); the package folder is deleted from this repository after Phase 0.5.
