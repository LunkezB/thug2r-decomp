# THUG2 Remix decomp — matching decompilation (C that compiles byte-identical to the shipped PSP binary) Cookbook

> **Evolvable reference (docs/ layer). Created 2026-10-11.** The compounding knowledge base for this project's recurring craft — the distilled techniques, idioms, and gotchas of the work you do over and over. Separate from the constitution (permanent) and the phase logs (granular history). **Consult this at session start before recurring work, and grow it after** (registry X4 — the flywheel). Append an entry every time you find a reusable nuance; the whole point is that each unit of work makes the next one cheaper and safer.

## Pinned context (the invariants every entry assumes)

- **Target:** *Tony Hawk's Underground 2: Remix*, PSP, the Feb 17, 2005 prototype — `BOOT.BIN` first, then any code modules on the same image.
- **CPU:** Allegrex — 32-bit little-endian MIPS with PSP-specific extensions and an FPU, plus the VFPU vector unit; instruction encodings must match the original assembler's.
- **Toolchain:** the pinned triple — TODO(phase-4); until then the candidates are Sony `psp-gcc`, SN Systems `pspsnc` and Metrowerks `mwccpsp`, and no entry may assume one of them.
- **Language:** TODO(phase-2) — C, C++ or mixed, decided from the bytes; entries say which language they apply to.
- **Split:** splat with its PSP platform; per-function assembly; translation-unit boundaries at the forced boundaries.
- **The gate:** an entry's lever is proven only when the function matches byte for byte AND the whole-binary hash stays green from a clean rebuild.
- **Inherited material:** the kit's PS1-era (gcc 2.7.2) levers do not transfer to the PSP compilers; their entry shape does — translate through the compiler pass, never copy the lever (G67).

## How to use this

1. **Before** a unit of recurring work, consult the entries below and shape the work toward the known idioms/recipes *first* — it saves rounds.
2. When you discover a new correspondence, technique, or "what makes X happen" trick, **add it here** — and, when applicable, also feed it back into the tooling (a flag, a script, a config entry) so the next similar case is even cheaper (X4). Don't over-encode genuine one-offs; the target is the *average* case trending toward one-shot plus a shrinking hard tail.
3. When a residual is a hard tail that no technique here reaches, note it, route it to the right escalation (permuter/tool-source research/human), and move on — don't grind (registry M8: exhaust the lever ladder, but don't force it past the machine-checkable gate).
4. Write entries **during the session that produced the insight** (X5) — a summary-only future session loses the detail that makes the entry correct.

## §1 — [First idiom / technique class]

*(The first entry lands here. Recommended entry shape: a short title, the trigger/situation, the technique, and a minimal example. Number sections `§1, §2, …`; append new phases' discoveries as new sections tagged with the phase that produced them.)*

<!-- Grow me. Each entry = a reusable lesson, captured in-session, cross-linked to the rule or tool it informs. -->

## The decomp entry shape (decomp-architect, installed 2026-10-11)

Every idiom entry is byte-proven on a named function and carries four parts:

1. **The residual** — what the diff looks like (the tell): the instruction, its position, the register, the count.
2. **The mechanism** — which compiler pass produces it and why, with the dump line that shows it (a verdict without a
   pass and a dump line is a hypothesis).
3. **The lever** — the C-level change that moves it, stated as a shape (never a register pin as the answer; a pin is a
   symptom). Before a lever enters this file, strip it from the accepted body and recompile: about one credited lever in
   three is inert.
4. **The byte proof** — the function, the diff before and after, the compilation the claim survived (standalone /
   real translation unit / whole-binary).

Pinned context for every entry: the toolchain triple `TODO(phase-4)` (TODO until Phase 4); the SDK evidence
(not yet inspected (no dump read at Phase 0.5); Phases 1-2 read the executable's module info, its import stubs (library names and NIDs) and any toolchain strings); the target's calling convention and register roles (TODO(phase-4)).

### The triage table (symptom → section) — the index a worker greps

| Tell in the diff | Likely mechanism | Lever family | Section |
|---|---|---|---|
| a temporary in a spill slot | a reload artifact | reshape the live range; declaration order | TODO |
| every small edit moves 20+ instructions | a register-pressure lock | hand to the permuter | TODO |
| a load stuck below a store while other loads float | an aliasing decision | the source's aliasing facts | TODO |
| a phantom callee-saved register | cross-call value caching / the allocation order | count the uses; re-shape | TODO |
| a shift off by ×4 against the target | the scaffold's pointer arithmetic | cast through a byte pointer | TODO |
| a branch's arms swapped | branch polarity | put the fall-through block in the `if` | TODO |
| a cross-jumped tail merged or not merged | the cross-jump count law | shape the shared block count | TODO |

*(Grow this table as the cookbook grows; a tool asserts every section is indexed and every index entry resolves.)*
