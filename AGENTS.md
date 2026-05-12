# Harvested

> A story of infrastructure powered by the souls of deceased

A story project built phase-by-phase with
[aiorchestra](https://github.com/ironharvy/AIOrchestra): each writing phase is a
GitHub issue, the agent opens a PR with one artifact, you review and merge it,
then the next phase's issue gets filed. **Read `WORKFLOW.md` for the full chain
and rules** — it governs how this repo is developed.

## Hard rules for anyone (human or agent) working here

1. **Read `story/` first.** Before writing anything, read every file under
   `story/`. The canonical state of the story lives there — not in issues, not
   in PR descriptions.
2. **One issue = one phase = one artifact.** Do the phase named in the issue
   title (routing table in `.aiorchestra/templates/implement.md` and
   `WORKFLOW.md`) and nothing else. Don't jump ahead.
3. **Never break canon.** Don't contradict `story/idea.md`, `story/premise.md`,
   `story/spine.md`, `story/world/*`, or any already-written chapter. New canon
   — names, places, the rules of this world, events — is welcome, but it must be
   consistent, and every new canonical fact (and every creative direction you
   considered and rejected) goes in `story/notes.md`.
4. **Keep the bookkeeping current.** Update `story/STATUS.md` every phase.
   Non-terminal phases file the next phase's issue with the `story` +
   `next-phase` labels only — a human adds `aiorchestra` + `claude` after
   reviewing the PR. That's the gate between phases.
5. **Story files are for the reader.** No meta commentary about phases / issues
   / PRs inside files under `story/` except `STATUS.md` and `notes.md`.
6. **The seed idea** (verbatim) is in `story/idea.md` under
   `## Seed (from README)` and at the top of `README.md`.

## Style

- **Register:** Literary but accessible — precise, concrete language; no purple prose, no minimalist affectation. Sentences vary in length. Technical and bureaucratic vocabulary (furnace maintenance, municipal procedure) is used naturally alongside emotional interiority.
- **POV:** Close third person, anchored to Lena Morrow. Other characters' inner states are revealed only through dialogue, action, and what Lena observes.
- **Tense:** Past tense.
- **Tone:** Sombre with dry, dark humour. The horror of soul-harvesting is rendered mundane (maintenance logs, union rules, shift changes); the emotional weight comes from specificity and understatement, not melodrama. Moments of genuine tenderness are earned sparingly.
- **Length target:** Novelette, ~12,000–18,000 words. Three acts, 9–12 chapters.
- **Constraints:** No info-dumps — world-building is woven through workplace detail, dialogue, and Lena's observations. Avoid archetypes of the "plucky rebel" or "chosen one"; Lena is a competent, complicit worker forced into action by a personal betrayal. The fantastical elements (souls as fuel, thanalic engineering) are treated as industrial fact, never as wonder or spectacle.

## Tooling

- `python story/_check.py` — the consistency gate aiorchestra runs at
  `validate`: a downstream artifact with real content must not sit on top of
  empty prerequisites, and an assembled `story/final.md` must be well-formed. It
  does not judge prose quality.
- `.claude/skills/herenow/` (if present) — used by the `Assemble & Publish`
  phase to publish `story/final.md`. Anonymous publishes are claimable for 24h;
  set `HERENOW_API_KEY` to publish under an account.
- If `scripts/run_qa.py` is present, the `Assemble & Publish` phase also runs it
  on `story/final.md` (name drift / character presence / cross-chapter phrase
  reuse).
