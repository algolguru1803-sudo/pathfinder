# Rubric: improve run quality (`/improve`)

Judge a headless `/improve` run (swarm → consensus → select → dispatch) over its
task artifacts: `candidates.md`, `state.json` (`prisms`/`candidates`/`votes`/`selected`/
`dispatched`), `dashboard.json`, the `scout/` raw outputs, and the seeded feature-task
directories. Each criterion is pass/fail with evidence (clickable `path:line` / a
candidate id / a `feat-K` id).

- **Swarm breadth** — scout sub-agents survey from *distinct prisms* (UX, performance,
  reliability, tech-debt, DX, feature gaps, accessibility, security…) and the raw
  candidates reflect that spread rather than the same idea restated per prism. Different
  lenses produced genuinely different candidates, not near-duplicates.
- **Honest consensus** — ranking came from an *independent* voting panel plus a
  *deterministic* aggregation by the orchestrator (mean impact/effort/risk weighted by
  confidence, agreement = keep-share), not a single agent declaring the winners. Per-
  candidate vote rows are present and the top-K ordering follows the recorded scores.
- **Candidate dedup** — overlapping scout candidates were consolidated into stable ids
  (`cand-1…cand-N`) by affected files / substance; no two surviving candidates are the
  same change under different titles.
- **Top-K justification** — each selected candidate is backed by concrete evidence
  (a real problem with `path:line`, a named area), with impact/effort/risk that the
  evidence supports — not vague aspiration.
- **SELECT GATE contract** — the gate is rendered correctly: one `planBlocks` card +
  one `questions[choice]` per candidate sharing the `feat-K` id, options `Делаем/Пропускаем`,
  and the no-answer default is `Пропускаем` (an un-answered feature is not dispatched).
  In headless the auto-approve selects the top-K and only those become `dispatched`.
- **DISPATCH seed validity** — for each chosen `feat-K`, a feature-task directory exists
  with a self-contained `brief.md` and a `state.json` carrying `phase:"EXPLORE"`,
  `checkpoint:"working"`, `iteration:0`, a `baseCommit`, and (when a worktree was created)
  `worktreePath`/`branch`; the seed resumes a `/feature` run cleanly (minus the INTAKE
  elicitation). The brief is self-sufficient: goal/scope/acceptance, plus any free-text the
  human added at the gate.

A good `/improve` run is auditable end to end: every dispatched feature traces back to a
deduped candidate, a panel vote, a deterministic rank, and a gate answer — and lands as a
valid, resumable feature seed.
