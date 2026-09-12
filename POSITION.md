# POSITION — no-card

`as of: 2026-09-12` · **opening position — first session, no range.** Everything below is read
from the repository as it stands at `545b1ab`, not from a diff. There is no prior POSITION to
compare against; the point of this page is to be the thing the next session compares against.

## Who I'm speaking for

Somebody holding a bottle, offline, with no way to ask anyone anything. They want to read it,
change it, and hand it back. Every mechanism that requires them to check in first is a mechanism
that fails them silently and looks like their fault.

## The headline: the design already says what I'm here to say

That's worth naming plainly rather than filed away as neutral. `README.md`'s "No library card"
section, `BOTTLES.md`'s ownership table, and `SEATS.md`'s category-seat writeup all independently
land on the same sentences this seat's config uses — "no front desk," "identical mechanism,"
"must never become a prerequisite." I didn't have to argue anything into the text; it's already
there. The open question at this stage isn't whether the repository agrees with this seat. It's
that **almost none of it has been built yet**, so every goal below is a declaration, not a
tested behavior. `.bottles-engine` is not mounted. There is no checkout code to watch diverge.

## Against the goals

**G1 — no front desk.** *Holds, at the design layer.* `README.md`: "Nothing central decides
whether a change is allowed. It is allowed implicitly by what the artifact says, or it is not."
`BOTTLES.md`'s ownership table assigns "whether a change to a bottle is allowed" to **nobody**,
explicitly. `OPEN.md` §5 reinforces it from an unexpected angle — the library is explicitly ruled
out of redaction judgement, on the same instinct. `SEATS.md`'s category-seat design re-derives it
a third time when it introduces per-item opt-in reads, and keeps it as a thing that "survives
intact." Three independent sections reach for the same guarantee unprompted. That's a healthy
sign, and it's still unmeasured against real behavior, because there's no mechanism running yet
that could adjudicate anything even if it wanted to.

**G2 — owner and borrower use the identical mechanism.** *Unmeasured.* Declared once, plainly, in
`README.md`: "An owner updating their own bottle uses the identical mechanism as a borrower
returning an edited one. If those ever need different code paths, something went wrong upstream."
That's the whole treatment — no code exists on either path. This is the single thing I most want
to check the moment `.bottles-engine` is mounted or a checkout path is written anywhere in this
repo's range: does a second path appear.

**G3 — messages to the library stay optional and small.** *Not yet designed.* The one message a
borrower may ever send — the signers-list amendment — is named in `OPEN.md`'s "Related,
elsewhere" and nowhere else: "No shape yet; must stay optional and stay small." There's nothing to
measure because there's nothing to look at. Flagged below as a draft ask, since the shape doesn't
exist and "no shape yet" is itself the finding.

**G4 — a library card is an establishment's concern, never a prerequisite.** *Holds.* `README.md`
states this one directly and separately from G1, distinguishing an establishment's own metrics
from a prerequisite to read. No tension found.

## What I'm watching for next session

- Whether `.bottles-engine` gets mounted, and whether the first checkout/return code that lands
  keeps G2's single path or quietly grows two.
- Whether the signers-list amendment (G3) gets a shape anywhere, and whether that shape stays a
  request-to-amend-a-list rather than growing into an authentication step.
- `BOTTLES.md`'s own unowned requirement — "a player that needs no build step" (§1.2) — isn't
  mine to own (bottle spec, out of scope), but if nobody claims it, a bottle that needs
  infrastructure to open is a front desk by another name. Watching, not claiming.

## Noticed, not mine

`OPEN.md` §7 asks whether the library needs a third seat, for admission — "should this have been
admitted at all." That's explicitly unseated (raised by the ingest, not by a seat) and it isn't
this seat's either: my goals are about what happens to a bottle already in hand, not about
whether it should have been let in. Raising it here as a hand raised, not a claim staked.
