# CURRENT_PHASE — Phase 0.5: decomp-architect: the decomp overlay

> The in-flight phase working file: the approved plan, the per-task checkpoint log, and blockers. **Copied from this template at Phase Start** (so the template is never overwritten); updated after every task; it is the crash/compaction recovery point and is in the Session Start load order. At phase close it is absorbed into `PhaseEnd_Phase[N].md` and `git mv`'d to `phase-ends/logs/PhaseLog_[N].md` (outside the load order). **Work accumulates commit-by-commit** — each task commits its changes together with its checkpoint entry here (P4), so this file never lags the code, and any task boundary is a clean handoff to a fresh session.

- **Started:** 2026-10-11
- **Effort baseline:** installer run (`decomp-architect/SETUP.md` Steps 1–10) — no per-task effort toggles in this harness
- **Context budget:** single session
- **Plan approved:** 2026-10-11 — the plan is exactly "execute SETUP.md Steps 1–10 in order" (Step 0.2)
- **Baseline state:** ProjectArchitect 2.0 installed and Phase 0 closed (`1c03cca`); nothing pushed

## Milestone (the phase's machine-checkable gate)

Step 10's verify list: the leftover-placeholder audit lists only ProjectArchitect's reference spec and its two phase templates; `python3 tools/audit_public.py` exits 0 (and failed on the planted fixture at Step 3); `bash -n tools/bootstrap.sh` is clean; the audit compiles without writing bytecode; `grep -c '^### G' RULES_REGISTRY.md` = 67; the package is gitignored; the install manifest is written; the PhaseEnd exists; this file is archived; both installer commits are present and trailer-free; the tree is clean.

## Task checklist

- [x] Step 1 — prerequisites: the version pin, the path, the registry precondition, the phase file
- [x] Step 2 — the game interview
- [x] Step 3 — the ROM firewall
- [x] Step 4 — the layout and its two READMEs
- [x] Step 5 — the bootstrap skeleton and the checkpoint commit
- [ ] Step 6 — the flywheel skeleton
- [ ] Step 7 — the registry: the decomp rules into §E
- [ ] Step 8 — the overlays and the skeletons
- [ ] Step 9 — the memory seed
- [ ] Step 10 — verify, the manifest, gitignore the package, close Phase 0.5

## Current task

**NOW:** Step 6
**NEXT:** Step 7
**Last rules check:** n/a (installer)

## Per-task checkpoint log

- **Step 1** — Every version-pin test passed (`docs/project-architect.md` carries the 2.0 version line; the registry, the constitution, `CLAUDE.md`, `PhaseEnd_Phase0.md`, both phase templates, the effort map, ops-setup, exactly one cookbook and `.claude-state/memory` exist). The ladder is in the constitution ("Governance and the firewall" found). §E holds no `### G` heading (only the one-line pointer), so Step 7 installs G1–G67 with no offset. Path A: no `src/*.c`, no `config/`, no `Makefile`. No Phase-0.5 file existed, so this one was created from the template.
- **Step 2** — The sixteen values. Read back from ProjectArchitect: PROJECT_NAME = THUG2 Remix decomp; COOKBOOK_NAME = matching-cookbook.md; INSTALL_DATE = 2026-10-11. Asked in one compact round (the developer confirmed the defaults offered, answered the rest, and accepted reading the serial from the image later):
  - GAME_TITLE = Tony Hawk's Underground 2: Remix
  - PLATFORM = PlayStation Portable (PSP)
  - GAME_SERIAL = the Feb 17, 2005 prototype build — serial to be read from the image's `PARAM.SFO` in Phase 1
  - TARGET_BINARY = BOOT.BIN
  - DUMP_PATH = /mnt/user-data/uploads (the cloud workspace's attachment folder, outside the repository; machine-local)
  - CONTAINER_LAYOUT = a UMD image (ISO 9660): `PSP_GAME/PARAM.SFO`; code in `PSP_GAME/SYSDIR` (`BOOT.BIN`, the unencrypted executable this build boots from, and `EBOOT.BIN`); game data in `PSP_GAME/USRDIR` in the game's own archive formats; any further code modules located in Phase 1
  - SDK_EVIDENCE = not yet inspected — no dump has been read at Phase 0.5; Phases 1–2 read the executable's module info, its import stubs (library names and NIDs) and any toolchain strings
  - COMPILER_FAMILY = the PSP compilers of 2004–05: Sony `psp-gcc` (GCC-based), SN Systems `pspsnc`, Metrowerks `mwccpsp` (all three are decomp.me candidates); possibly mixed per module; C and/or C++
  - COMMUNITY_WORK = no public decompilation of the PSP version found on 2026-10-11; the Feb 17, 2005 prototype is documented by Hidden Palace; a fan-made "Revision + Re-Dub" ROM hack of the Remix exists
  - PROJECT_GOALS = a matching decompilation of the Feb 17, 2005 prototype's `BOOT.BIN` (and any code modules on the image) to 100% source, byte-identical; to make the Remix-exclusive content — levels, characters and cutscenes absent from the PC version of Underground 2 — readable in source; and to build PSP decompilation methods and tools that transfer to other PSP games. The US and EU retail builds follow as additional configurations.
  - LICENSE_CHOICE = MIT for the project's own tools and documentation; no license is asserted over the decompiled source, which describes a work the project does not own
  - AI_DISCLOSURE = This project is developed with substantial assistance from Anthropic's Claude; every match is verified by a byte-identical build, and names and public-facing text are reviewed by a person.
  - PUBLIC_OR_PRIVATE = public from the first push (2026-10-11)
  Verified: all sixteen non-empty; DUMP_PATH is absolute and not under the repository root; `docs/matching-cookbook.md` exists.
- **Step 3** — The firewall, in force from this commit. 3.0: ProjectArchitect's bare `.run/` line rewritten to `/.run/*` (the one edit above a marker). The kit's ignore block appended under its dated marker; `config/firewall.txt` (first purge path `BOOT.BIN`), `config/firewall-fixture.sha1`, `tools/audit_public.py` and `.github/workflows/no-rom.yml` copied verbatim. Negative control: the audit on the planted fixture exited 1 naming `OFFENDER .run/firewall-control/planted.bin`; after removing it, the audit on the tree exited 0 (three loud warnings for the pending hash sources of Phases 1 and 3, as designed). All eight positive and five negative ignore probes behaved as listed; the transcripts rule is the tracked `.gitignore`'s, not only the local exclude. Finding: the kit's ignore block has no PSP-specific patterns (image files `*.iso`/`*.cso`, a stray `BOOT.BIN`/`EBOOT.BIN`/`*.prx` outside `disks/` and `extracted/`) — the dump lives outside the repository, so nothing is exposed now; recorded as a `TODO(platform)` for Phase 1.
- **Step 4** — The layout directories created; `docs/README.md` and `.run/README.md` copied and filled. Verified: no placeholder left in either; `.run/README.md` is trackable.
- **Step 5** — `tools/bootstrap.sh` copied (a skeleton whose TODOs are phase tasks); `bash -n` clean. Checkpoint commit by explicit path.

## Blockers / open questions

- none

## Notes / deviations

- Same harness as Phase 0 (claude.ai cloud workspace): no fresh session between the two installers; the developer directed continuing.
