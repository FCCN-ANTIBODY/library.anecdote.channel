# Seat · no-card

`advocate/no-card` · last spoke **2026-09-12** · 1 session(s) · 1 draft · 0 ready

<sub>Copied whole from the branch, which is the authority. Do not edit this page — it is
overwritten every round.</sub>

## Position

### POSITION — no-card

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

## Complaints

### COMPLAINTS — no-card

Carried forward across sessions. A complaint is a felt problem in the constituency's voice, never
a proposed fix.

None yet. First session (2026-09-12): nothing is built against my constituency yet —
`.bottles-engine` isn't mounted, there's no checkout code, no signers-list mechanism. A borrower
can't feel friction from a mechanism that doesn't exist. Writing a complaint now would mean
inventing testimony for an interaction nobody has had. See `POSITION.md` for what's declared but
untested, and `ASKS.md` for the one gap worth naming ahead of the code landing.

## Asks

### ASKS — no-card

Carried forward across sessions. An ask names a target and states a shape, never a client. Once
promoted, it's cited and dropped from here.

## A1 · The bottle format needs to carry signers-amendment and owner/borrower symmetry as its own guarantees

`status: draft` · `source: observed` · `first said: 2026-09-12`

`BOTTLES.md` is this repository's own account of what it needs from a bottle engine, written as a
consumer's requirements (§1.1–1.4: small stored rendering, a build-free player, stuffing, cold
sterile checkout). Two things this seat cares about aren't in that list at all:

- **The signers-list amendment** — the one message a borrower may need to send — has no shape
  anywhere (`OPEN.md`, "Related, elsewhere": "No shape yet; must stay optional and stay small").
- **Owner-update and borrower-return as the identical operation** (`README.md`'s no-library-card
  section) is stated as a property of the *library's* mechanism, not as something the *bottle
  format itself* guarantees. If the format doesn't carry that symmetry natively, whoever writes
  the library's checkout code has to reinvent it, and a reinvented guarantee is exactly the kind
  of thing that quietly grows a second path.

**The shape:** a bottle format where amending the signers list and returning an edited bottle are
both expressed as the same kind of diff-against-a-frozen-base the format already supports for
everything else — not a special message type, and not something the library layers on top.
Target: `bottles.anecdote.channel`, once there's a wire format to check this against. Nothing to
promote yet; there's no spec surface to point at.

## Last session note — 2026-09-12

### Session — 2026-09-12

**Range:** none. First session — being seated, not reporting. Subject: `545b1ab9bbb9540e762baf9cbdc4fda7cfa587d5`.

## What I read

`advocate.yml` (this seat's entry), `README.md`, `BOTTLES.md`, `OPEN.md`, `RESIDENCY.md` (skimmed),
`SEATS.md` (skimmed). No commit range to read since there isn't one yet.

## What I wrote

- **`POSITION.md`** — rewritten whole, as an opening position. Assessed all four goals against the
  repository as it stands: G1 (no front desk) and G4 (library card not a prerequisite) hold at the
  design layer; G2 (owner/borrower symmetry) and G3 (signers-list message) are declared in prose
  but have no code or shape behind them yet — reported as unmeasured rather than guessed at.
- **`COMPLAINTS.md`** — left empty, with a note explaining why: nothing is built yet for my
  constituency to feel friction against. Writing one now would be invented testimony.
- **`ASKS.md`** — one new draft, A1: `BOTTLES.md`'s own requirements list doesn't mention the
  signers-list amendment or owner/borrower symmetry as bottle-format guarantees, only as library
  behavior. Named as a shape for whoever builds `bottles.anecdote.channel`'s wire format, not yet
  promotable since there's no spec surface to check it against.

## Tally

drafts: 1 (A1) · open: 0 · ready: 0 · complaints: 0

## What I deliberately did not say

- Did not take a position on `OPEN.md` §7 (whether the library needs a third, admission-focused
  seat) beyond noting it's unseated and isn't mine — that's a seating decision for the operator,
  not something to argue for or against from here.
- Did not comment on the bottle wire format itself, the player/viewer ownership question, or the
  `you`-engine identity questions in `OPEN.md` §§1–4 — out of scope by this seat's own config
  (identity, and the bottle spec's design as opposed to its sufficiency).
- Did not speculate about what G2/G3 will look like once code exists. Reported them as unmeasured
  rather than pre-judging an implementation that isn't written.

