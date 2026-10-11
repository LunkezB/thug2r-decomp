# phase-ends/DIGEST.md — the session-start digest (every phase in one page)

> **Purpose.** The Session Start Protocol reads the constitution, the registry (every rule in full), THIS file, the
> three most recent PhaseEnds in full, and `CURRENT_PHASE.md`; it does not read every PhaseEnd once more than three
> exist. This file therefore carries a synopsis of every phase and the corrections that supersede parts of the
> permanent constitution. The PhaseEnd files stay the durable record — read an older one on demand when a synopsis
> is not enough. **Maintenance:** at every PhaseEnd, append that phase's synopsis here (a phase-close checkbox).
> This file is DERIVED from the PhaseEnds and may be corrected; the constitution is never edited.
> Installed by decomp-architect on 2026-10-11.

## 0. Where the project stands (at the latest PhaseEnd — the live state is in CURRENT_PHASE.md)
**At PhaseEnd 0.5 (2026-10-11, v0.2.0):** governance and the decomp overlay are installed — the ROM audit fails on its planted fixture and passes on the tree, and the registry holds G1–G67. The first push (`2dd9e12`) ran the no-ROM CI green (GitHub Actions run 38170013331), which completes Phase 0's ladder milestone. No game file has been read yet: no numbers exist. Next is Phase 1 (deterministic extraction), opened by three cheap reads of the developer's image: the serial, the integrity of the repaired image around `BOOT.BIN`, and whether `BOOT.BIN` carries symbols.

(one paragraph, rewritten at every PhaseEnd: the last milestone met, the numbers as generated, what is next)

## 1. Corrections and supersessions of the constitution recorded in PhaseEnds
(one bullet per correction: what the constitution says, what is true now, which PhaseEnd recorded it)
- none yet.

## 2. Phase synopses (what each phase delivered, its key finding, the rules it added)
**P0 (2026-10-11, v0.1.0) Governance install.** ProjectArchitect 2.0.0 was installed (recovered from its repository's history because the kit pins 2.0) and the constitution was generated from the kit's intake — Phases 0–10 adapted to the PSP, with the developer a beginner, the repository public and the target the Feb 17, 2005 prototype's `BOOT.BIN`; no rules added.

**P0.5 (2026-10-11, v0.2.0) The decomp overlay.** The decomp-architect kit installed as specified: the ROM firewall (the ignore block, `config/firewall.txt`, `tools/audit_public.py` proven against a planted fixture, the no-ROM CI), registry §E G1–G67, the CLAUDE/effort-map/cookbook/ops-setup overlays, the kernels and the dictionaries' front pages, 18 memory seeds and the README/LICENSE/NOTICE/CONTRIBUTING skeletons. Key finding: the kit's kernels file says 80 kernels but holds 81 (an upstream slip; the copy is complete). Two `TODO(platform)` items recorded: PSP-specific ignore patterns (Phase 1) and C++ file types in `make format` (Phase 4). Rules added: G1–G67.

(one paragraph per phase, appended at its close)

## 3. Where things live (the document map a session needs)
(the wiki's reference index first; then the files a session touches most: the ops reference, the cookbook and its
index, the codegen map, the wave runbook, the effort map, the decision log, the accelerators, the address ledger,
the formats, the pinned-walls list, the archived worklogs — on demand only)
