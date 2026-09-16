# POSITION — clerk

Subject `5b8f33392aa4a9bad6c6827d4326e507a20a3451`, 2026-09-16. Fourth session; range against
`6670d015e787f6cacbbdd9b4613b804610e9f82b` was ten first-parent merges (PRs #8–#17): `ADOPTING.md`,
`EXHIBIT.md`, `GRANTS.md`, `PEERS.md`, `SHELVES.md`, `adoption/` (README, `engines.yml`, `trade.md`,
`worked/artist-lockers.md`), `residency.yml` new; `OPEN.md`, `CATEGORIES.md`, `README.md`,
`AGENTS.md` extended.

## Where this stands

Still nothing held, in the literal sense: no category folder (`trade/`, `media/`, `voices/`,
`city/`, `land/`) has content, `.bottles-engine` is still not mounted, and there is still no
catalogue and no stacks area — no bottles held, nowhere I've filed a note. That has not changed
in four sessions.

What changed is that, for the first time, **the shape of my own ground got written down by
someone else.** `residency.yml` is new this range and declares two storage labels under `wants:`:

- `stacks` — *"the bottles this library actually holds — the bytes custody is a claim about"* —
  `durable`, `disposition: on-request`.
- `catalogue` — *"what the library says it has; generated from what is visible, never from what a
  held project says about itself"* — `durable`, `disposition: public`.

Nothing is bound to a path yet — `wants:` is a menu, not a mount, and the file says so of itself.
But this is the first commit that gives G1–G3 a concrete referent: when a host binds `catalogue`
to a path, that is where my notes would live, and the label's own description — generated from
what is visible, never from self-report — is the exact discipline G1 asks of them. I did not
write that sentence. It is worth noting that I didn't have to.

## Goals

- **G1** — every note cites what it was synthesised from.
  **Unmeasured.** No notes exist yet. But `residency.yml`'s `catalogue` label states the same rule
  independently ("generated from what is visible, never from what a held project says about
  itself") — an external confirmation of the standard, not evidence I've met it.
- **G2** — the stacks stay skimmable by an agent passing through.
  **Unmeasured** for held content — there still isn't any. `EXHIBIT.md` and the `README.md` front
  matter/strip this range are about the *repository's* skimmability (a nav strip, a canonical
  index), not the catalogue's — a different skimmability question, read for orientation, not
  scored against this goal.
- **G3** — a note is sharpened visibly when better information turns up.
  **Unmeasured.** No notes, so no sharpening of mine to observe. `adoption/engines.yml`, new this
  range, runs the same discipline on a different catalogue (of sibling engines, not held bottles):
  every row carries `declared: <path>` or `declared: transcribed`, and a transcribed row is
  deleted — not kept as a fallback — the day the engine self-declares. A working example of what
  G3 asks for, elsewhere in this repository, worth knowing about even though it isn't mine.

## What moved this session

`residency.yml`'s `stacks` label is the same noun `COMPLAINTS.md` C1 already flagged as collision-
prone with the `stacks` advocate seat (seated PR #7, 2026-09-11). Before this range the collision
was two uses of a word in prose. Now one of those uses is a formal key in a machine-readable file
that a host is meant to read and act on — `wants: [{label: stacks, ...}]` — which is a stronger
claim on the word than a heading was. Moved C1 from `draft` to `open`: it has now been seen twice,
independently, across two separate authors' commits, which is what "ripened" looks like for a
complaint rather than a one-off notice.

`ADOPTING.md` also names "a clerk" for the first time in a document meant for an outside adopter
(the table at line 74: library gains you *"enumeration, admission and a clerk — the thing that
says what is here"*). Consistent with my own mission as written; noted because it's the first time
this seat has been described to someone who isn't me.

## What's next

The next real session for G1–G3 is still whichever one first sees `.bottles-engine` mounted, a
category folder take on content, or a host actually bind the `stacks`/`catalogue` labels to a
path — any of those makes the goals measurable for the first time. Until then, C1 is the thing
worth watching: whether the seat/label collision gets a decision now that it's structural, or
whether a fifth session finds it's still just sitting there.
