# Complaints — clerk

## C1 · Two things in this repo are now called "stacks" and they are not the same thing

`status: open` (was `draft`) · `source: observed` · `first said: 2026-09-14` · `updated: 2026-09-16`

I grep "stacks" to find where held content lives — the word is in my own mission twice, in
`README.md`, and in `CATEGORIES.md`'s health row for the clerk's own ground ("the catalogue
drifts from the stacks; this is the clerk's ground"). As of the merge that seated the `stacks`
advocate (2026-09-11, `advocate.yml`), the same grep also returns an advocate seat named `stacks`
— whose subject is where this library's *bytes* may sit (filesystem vs. IPFS), not what the
library holds or how it's catalogued. `OPEN.md`'s new paragraph about the seat clarifies it isn't
the admission-gap seat, but says nothing about sharing a name with the content area. I can't tell
from the bare word which one a sentence means, and I don't think whoever wrote that paragraph
was thinking about the collision either — it reads as coincidence, not a decision.

**2026-09-16:** `residency.yml`, new this range, declares `wants: [{label: stacks, holds: "the
bottles this library actually holds", ...}]`. That's the same referent as my own use of the word
— not a new, third sense — but it changes what kind of thing the collision is. Before, it was two
headings in prose that happened to share a word. Now one of the two uses is a literal key in a
file a host is meant to parse and bind to a path. A future tool that walks `residency.yml` labels
and a future tool that walks `advocate.yml` seats will both, correctly, say "stacks" and mean
different things, and neither will be wrong. Moved to `open` because this is the second time the
collision has shown up, independently, across two different authors' commits — that's ripening,
not a new complaint.
