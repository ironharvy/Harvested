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

- **Prose register:** Literary speculative fiction. Precise, unadorned, mid-register — closer to Kazuo Ishiguro or Kelly Link than to pulp sci-fi. Sentences earn their length; no purple prose, no minimalist affectation.
- **POV:** Close third person, locked to Maren Voss.
- **Tense:** Past tense.
- **Tone:** Melancholy, restrained, and quietly horrifying. The world's monstrousness is presented as mundane because to its inhabitants it is. Moments of warmth exist but are brief and hard-won.
- **Length target:** Short story / novelette, roughly 8,000–12,000 words.
- **Stylistic constraints:**
  - No info-dumps; world-building is revealed through Maren's routine and small physical details (the hum of a containment cell, the form she stamps, the colour of a degraded readout).
  - Dialogue is spare and functional — people in bureaucracies don't monologue.
  - The supernatural elements (souls, ghost lights, psychic energy) are treated as engineering facts, not mystical wonders. Technical language is used the way workers use jargon: without awe.
  - Horror lives in implication and normalisation, never in graphic depiction.
  - The ending is bittersweet and ambiguous — no triumphant system-toppling, no nihilistic despair.

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
