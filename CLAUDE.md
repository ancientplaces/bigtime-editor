# bigtime-editor — Claude Code project rules

**Repo:** `ancientplaces/bigtime-editor` · **Class:** CODE serving Pages —
**the DEPLOY contents rule governs this repo**
**Visibility:** **PUBLIC** (verified 2026-08-04 via `gh repo view`). Pages
`built`, served from `main` `/` at https://ancientplaces.github.io/bigtime-editor/
(verified 2026-08-04 via `gh api repos/ancientplaces/bigtime-editor/pages`)
**Local path:** `/Users/leehoward/Documents/Claude/Projects/Music-related software development/bigtime-editor` (verified 2026-08-04 via `pwd`)
**Purpose:** The Big Time MIDI editor — a single self-contained `index.html`
web app for the Chase Bliss Big Time delay, plus its user-facing docs and the
locked MIDI spec PDF. No build step, no dependencies beyond a Google Fonts link.

Global rules: `~/.claude/CLAUDE.md`. Doctrine:
`github-residence-canonical-2026-07-26-r3.md` as amended by
`cc-port-ruling-2026-08-04.md`, both in `ancientplaces/groundwork-store`.

## Contents rule — this repo is public

Application source and user-facing material only. The whitelist, as tracked
2026-08-04:

| File | Role |
|---|---|
| `index.html` | The app — single self-contained file |
| `README.md` | Public front door |
| `USER-GUIDE.md` | User-facing guide |
| `CHANGES-SPEC.md` | User-facing change/spec notes |
| `Big-Time-MIDI-manual-locked-2026.pdf` | The locked MIDI spec (ref 2026 – BT001) |

**No internal docs, ever. No session logs, no handoffs, no kickoffs, no
status files, no ledgers, no secrets, no tokens.** Every byte here is world
-readable the moment it is pushed. A file whose audience is Lee or a future
session does not belong in this repo — it belongs in
`cb-controllers/bigtime/` (see below).

Deploys follow `github-deploy-runbook-2026-08-04.md` in groundwork-store.

## Internal docs live elsewhere

The Big Time project's internal documentation is **not** in this repo. It
lives in `ancientplaces/cb-controllers` (PRIVATE, class STORE) under
`bigtime/` — 10 files as of 2026-08-04, including `PROJECT-HANDOFF.md`,
which was moved out of *this* working tree on 2026-08-04 precisely because
it is internal and this repo is public.

Write internal Big Time material to `cb-controllers/bigtime/`. Never
relocate it back here.

## Session discipline

- Start of any session that will commit: `git status -sb` after a fetch;
  behind → pull; diverged or unexplained dirty tree → stop and report.
- Commit messages name what actually changed.
- **This repo takes no session log** — it is a public deploy surface. A
  session that touches it appends its dated line to `session-log.md` in
  `ancientplaces/groundwork-store` instead.
- Deletions only on Lee's written instruction naming the file.
- An untracked file appearing in this tree is a **stop condition**, not a
  thing to commit. Determine what it is before `git add` — that is how
  `PROJECT-HANDOFF.md` was caught rather than published.

## Project-local rules

- **Open return leg, 2026-07-21 — the built `index.html` never landed.**
  A build produced on 2026-07-21 was never committed here. Verified again
  2026-08-04: `index.html` was last changed **2026-06-25** by `5a482e3`
  ("Add user guide + header link to it"), and HEAD is still `5a482e3`. The
  deployed page is therefore the 2026-06-25 build, not the 07-21 one.
  **Check date: 2026-08-11** — a deadline, not a waiting period. On that
  date: either land the 07-21 build or record that it is abandoned. A leg
  past its date without a written outcome is dead, not pending.

## Chat counterpart

The Music-related software development Chat project is planning-only
(option A, 2026-08-04). Files it produces arrive via its §16 queue. Anything
internal it produces goes to `cb-controllers/bigtime/`, not here. Its
knowledge cache is non-authoritative — this repo wins.
