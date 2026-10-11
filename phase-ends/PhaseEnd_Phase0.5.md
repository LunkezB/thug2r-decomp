# PhaseEnd — Phase 0.5: decomp-architect: the decomp overlay

**Date:** 2026-10-11 · **Project Version:** 0.2.0 · **Phase Status:** Complete

> Written only at a developer-confirmed milestone (Tier-1 task, `/effort max`). This is the durable synthesis a fresh session reads — write it as if `CURRENT_PHASE.md` will never be read again (it is archived to `phase-ends/logs/`, out of the load order). Keep it lean: non-derivable content only (target ≤30 KB).

## Build Log

**Files created/changed and complete — do not recreate** (the install manifest, `.run/decomp-architect-install-manifest.txt`):

```
APPENDED .claude-state/memory/MEMORY.md (## decomp-architect seed)
APPENDED .gitignore (# ROM firewall — in force from the FIRST commit; # decomp-architect (the day-one kit's package folder — safe to delete after install))
APPENDED CLAUDE.md (## Decomp fail-safes)
APPENDED RULES_REGISTRY.md (## §E — Project-specific rules (a matching decompilation))
APPENDED docs/effort-map.md (## Per-phase effort map (decomp ladder)
APPENDED docs/matching-cookbook.md (## The decomp entry shape)
APPENDED docs/ops-setup.md (## Decomp environment)
APPENDED phase-ends/CURRENT_PHASE.template.md (## 🛑 SESSION CHECKPOINT)
APPENDED phase-ends/PhaseEnd.template.md (## What we believed, what failed and why it looked right, what it cost, and what we would do sooner)
CREATED .claude-state/memory/<the kit's 18 seed files>
CREATED .clang-format
CREATED .github/workflows/no-rom.yml
CREATED .run/README.md
CREATED .run/decomp-architect-install-manifest.txt
CREATED CONTRIBUTING.md
CREATED LICENSE
CREATED Makefile
CREATED README.md
CREATED config/decomp-hooks.snippet.json
CREATED config/firewall-fixture.sha1
CREATED config/firewall.txt
CREATED config/mcp.json.template
CREATED docs/README.md
CREATED docs/decomp-architect.md
CREATED docs/decomp-kernels.md
CREATED docs/inherited-record.md
CREATED docs/knowledge-corpus.md
CREATED docs/tools-manifest.md
CREATED docs/wave-playbook.md
CREATED phase-ends/DIGEST.md
CREATED phase-ends/PhaseEnd_Phase0.5.md
CREATED phase-ends/logs/PhaseLog_0.5.md
CREATED src/NOTICE.md
CREATED tools/audit_public.py
CREATED tools/bootstrap.sh
SKIPPED .claude/settings.json (never touched at Phase 0.5)
SKIPPED .mcp.json (never touched at Phase 0.5)
SKIPPED CONTRIBUTING.decomp-skeleton.md (no existing CONTRIBUTING.md; the skeleton was created as CONTRIBUTING.md)
SKIPPED README.decomp-skeleton.md (no existing README.md; the skeleton was created as README.md)
SKIPPED docs/decomp-ladder.md (the ladder is in the constitution; Step 1.3 passed)
```

The manifest file itself lists the 18 memory files by name; it lives in ignored scratch and is regenerable from this list.

**Tools/packages installed:** None. The installer stamps documents, configuration and one script (`tools/audit_public.py`); the extractor, the oracles, the build and the compiler are Phases 1–4.

**Verification results:**
- The firewall's negative control: the audit on the planted fixture exited 1 with `OFFENDER .run/firewall-control/planted.bin`; on the tracked tree it exited 0 (three loud warnings for the pending hash sources of Phases 1 and 3, by design).
- The ignore probes: 8 of 8 positive paths ignored, 5 of 5 negative paths trackable; the transcripts rule comes from the tracked `.gitignore`.
- `grep -c '^### G' RULES_REGISTRY.md` = 67; the marker once; no offset.
- The placeholder audit: only `docs/project-architect.md`. `bash -n tools/bootstrap.sh` clean; the audit compiles without bytecode; both JSON templates parse; 34 memory seeds with every index link resolving; 15 `TODO(phase-` lines in ops-setup.
- One count check failed as written (see Deviations): `docs/decomp-kernels.md` has 81 kernel headings against its own stale "80" figure; the file is byte-identical to the kit's and DK-1…DK-81 are each present once.

**Milestone achieved:** the Step 10 verify list holds — the audit fails on the planted fixture and passes on the tree, the registry holds G1–G67, every overlay is in place, the package is gitignored, and the tree is clean. Phase 0's ladder milestone completes with the first push (the no-ROM CI green on it).

**Next:** Phase 1 — Deterministic extraction with a committed manifest. Start with the plan (Plan mode, Max); its first tasks are the three cheap reads of the image (the serial from `PARAM.SFO`, the integrity of the repaired image around `BOOT.BIN`, whether `BOOT.BIN` carries symbols). The developer attaches the image first.

## Deviations

| Item | Plan | Actual | Reason |
|---|---|---|---|
| Fresh session before the kit | a new Claude Code session after Phase 0's hard stop | continued in the same conversation | the claude.ai harness has no session restart; the developer directed continuing |
| Step 6 kernel count check | `grep -c '^### DK-'` equals the file's "In all" figure | 81 vs 80 | an upstream slip in the kit: DK-81 was added without updating its Coverage line (the kit's README and wiki say DK-1…DK-81); the copy is byte-identical and complete, left unedited |
| Kit master copy location (an ops-setup row marked for Phase 0.5) | an absolute local path | the pinned GitHub location of the kit (BFM-decomp commit `e63ef6b`) | the cloud workspace keeps no local copy between sessions |
| `LICENSE` | the skeleton, replaced by the developer before the first push | the skeleton committed here; replaced by the MIT text in the next commit, before the push | the developer chose MIT and directed the push |
| PSP-specific ignore patterns | — | not added (the kit's block is copied verbatim) | recorded as `TODO(platform)` for Phase 1: image files (`*.iso`, `*.cso`) and stray executables/modules outside `disks/` and `extracted/`; the dump lives outside the repository, so nothing is exposed now |
| `make format` coverage | — | `*.c`/`*.h` only | recorded as `TODO(platform)` for Phase 4: add `*.cpp`/`*.hpp` if Phase 2 finds C++ |

## What we believed, what failed and why it looked right, what it cost, and what we would do sooner

- **Believed:** the kit's installer would run unmodified on a fresh ProjectArchitect 2.0 install, with every self-check
  passing. **True / false:** true except one bookkeeping check — the kernels file's typed total lagged its content by one
  kernel. **Sooner:** the kit's own health check (it asserts its dictionaries equal their sources) evidently does not cover
  that Coverage line; a derived figure there would have caught it upstream.
- **Failed, and why it looked right:** nothing failed in this project's tree; the one red check was a stale typed number
  in the kit, and the copy it guarded was complete. It looked right upstream because the README and the wiki were updated
  and the figure in the file was not — exactly the "typed figure vs derived figure" failure the kit's own accelerators
  list names.
- **Cost:** a few minutes of verification (a byte comparison and a numbering check); no rework.

## Commit Message

```
chore: decomp-architect Phase 0.5 — the decomp overlay installed
```
*(No `Co-Authored-By` / AI-attribution trailer — H5.)*

## Rules Added This Phase

| Rule | Reason |
|---|---|
| G1–G67 installed into §E — the kit's seed | the origin of each is its `provenance:` line |

## PhaseEnd Changelog

`v0.1.0 → v0.2.0` — the decomp overlay: the ROM firewall with its negative control and CI, the layout, registry §E G1–G67, the overlays, the kernels and the dictionaries' front pages, 18 memory seeds, the skeletons.

## Plain-English Recap

This phase installed the decompilation-specific half of the rulebook. The most important part is the "firewall": a set of
ignore rules plus a checking script (`tools/audit_public.py`) that refuses any file that came from the game — and it was
proven to work by planting a fake game file and watching the check fail on it. The registry gained 67 rules (G1–G67)
learned the hard way by a project that finished a full matching decompilation, and the documents now carry that project's
lessons, its work procedure and the list of tools to build. Nothing from the game is in the repository; the next phase
starts the real work by unpacking your copy of the game image.
