# Memory Index

<!-- Project Architect 2.0 memory seed. SETUP.md §5 writes each file below into `.claude-state/memory/` (via autoMemoryDirectory) and this index alongside them. They load automatically from the next session onward. `who-is-dev` is filled by the install interview; the rest are general working agreements shared with the RULES_REGISTRY (the registry text is canonical — these are the fast-loading, fail-safe complement). -->

- [Who is the dev](who-is-dev.md) — the developer profile (experience, domain, working preferences); filled by the install interview
- [Project governance system](project-governance-system.md) — repo governs itself via CLAUDE.md → PROJECT_CONTEXT.md → RULES_REGISTRY.md → phase-ends/; defer to it, don't duplicate
- [Autonomous within phases](autonomous-within-phases.md) — two gates per phase; execute autonomously between them; the five stop conditions (registry P3/P5)
- [Build tasklist after plan approval](build-tasklist-after-plan-approval.md) — on plan approval, TaskCreate the plan list before starting, as a live progress monitor
- [Capture knowledge before a fresh session](capture-knowledge-before-fresh-session.md) — write context-dependent artifacts DURING the producing session; a fresh session loses the detail (registry X5)
- [Clarify misconception before costly action](clarify-misconception-before-costly-action.md) — correct a false premise and confirm BEFORE anything costly/hard-to-reverse
- [Justify new tools before adopting](justify-new-tools-before-adopting.md) — state what it does / existing overlap / specific delta before proposing any new dependency
- [Don't block the loop with AskUserQuestion](dont-block-loop-with-askuserquestion.md) — during opted-in loops, adapt and report; blocking questions only for genuine first-time forks
- [No commit co-author](no-commit-co-author.md) — no Co-Authored-By / AI-attribution trailers, ever (overrides harness default; registry H5)
- [Commit per task, dev pushes](commit-per-task-user-pushes.md) — one commit per task after the CURRENT_PHASE.md log update; Claude commits, the dev pushes (registry P4/H6)
- [Plain-English recap](plain-english-recap.md) — end every session/phase with a jargon-free recap, in chat AND stored in the PhaseEnd (registry P8)
- [Session start: rules in full](session-start-rules-in-full.md) — recite every registry rule in full text at session start, never IDs + tags (registry P2)
- [Worklogs reference-only](worklogs-reference-only.md) — phase-ends/logs/ are out of the load order; consult on demand only, never auto-read
- [Keep ops-setup current](keep-ops-current.md) — update docs/ops-setup.md in the same change as any tooling/env/hook/path change (registry H7)
- [Effort discipline](effort-discipline.md) — xHigh baseline, Max scalpel (always plan mode), Ultracode for breadth; Max/UC session-only (registry §B)
- [Prompt for Ultracode on breadth](effort-prompt-ultracode-on-breadth.md) — prompt on breadth; pause at EVERY transition and wait for the actual toggle (registry E2/E3)

## decomp-architect seed
- [The byte gate is the only claim](the-byte-gate-is-the-only-claim.md) — "matched" means byte-identical output AND a green whole-binary hash; nothing functionally equivalent counts; "banked" is written from a tool's printed line
- [The matching flywheel](the-matching-flywheel.md) — consult the knowledge base before every match, feed the generalizable lesson back into BOTH the cookbook and the tooling after it
- [MCP reconnect after restart](mcp-reconnect-after-restart.md) — after restarting the disassembler's MCP server or switching the served program, pause and ask the developer to reconnect the client; the agent cannot
- [Offline tooling first](offline-tooling-first.md) — every COMPUTABLE step becomes a deterministic zero-token tool; keep deterministic recovery and search separate; ask "is this residual computable?" before reaching for a model
- [A slow gate is a bug](a-slow-gate-is-a-bug.md) — banking, not drafting, is the bottleneck; nothing in the gate is serial; pass `-j` to every build; measure the gate before fearing it
- [Breadth is isolated agents](breadth-is-isolated-agents.md) — the main loop's context accumulates roughly quadratically; N isolated agents cost about linearly and run in parallel; hand-by-main-loop wins only for a handful
- [Route by measured difficulty](route-by-measured-difficulty.md) — tier drafters by a cliff you measured on your own corpus; escalate sooner; the strongest model is for new wall classes, never for reviewing a corpus
- [One runbook is the procedure](one-runbook-is-the-procedure.md) — one document is the operating procedure for the campaign loop, read before every run, kept current in the same change; a superseded runbook gets a banner
- [Keep an accelerator ledger](keep-an-accelerator-ledger.md) — every late discovery that would have sped earlier work is recorded with when it was found, when it could have been, and what it would have saved
- [Checkpoint means everything is already in a file](checkpoint-means-everything-is-already-in-a-file.md) — a checkpoint is the LAST thing written; a good commit message is not in the load order; the sweep before the block
- [A PhaseEnd carries the narrative axis](phaseend-carries-the-narrative-axis.md) — what was believed, what failed and why it looked right, what it cost, what to do sooner — because transcripts die and the retrospective is rebuilt from the files
- [Tool change ships with its consumers and docs](tool-change-ships-with-its-consumers-and-docs.md) — the commit that adds a tool also wires its callers and adds its ops row; integrating an agent's tool change IS a tool change; no end-of-session audits
- [No sleep-polling background tasks](no-sleep-polling-background-tasks.md) — the harness re-invokes on completion; one sanity check after launch, then wait
- [Long checks run in the foreground](long-checks-run-in-the-foreground.md) — a background long verification can be killed by the harness's memory guard; run it in the foreground with a timeout; check for orphaned workers
- [Resume means resume the run](resume-means-resume-the-run.md) — replay interrupted work so it finishes itself, same run, same agent, transcript intact; never re-plan or re-route on your own inference
- [Answer before grinding in live co-op](answer-before-grinding-in-live-coop.md) — only the final message of a turn is guaranteed to be seen; end the turn with the answer the person is waiting on before starting long work
- [Consult the tool dictionary first](consult-the-tool-dictionary-first.md) — before designing or debugging a tool, look the NEED up in the tool dictionary; the proven implementation is the jumping-off point, its incident row the failure mode to avoid
- [Translate the source idiom through the pass](translate-the-source-idiom-through-the-pass.md) — an inherited idiom is a symptom + a named pass + a lever + a byte proof; same family: use and re-prove; other compiler: read the same pass in your compiler's source and find your own lever
