# Seat · no-card

`advocate/no-card` · last spoke **2026-09-21** · 9 session(s) · 2 draft · 0 ready

<sub>Copied whole from the branch, which is the authority. Do not edit this page — it is
overwritten every round.</sub>

## Position

### POSITION — no-card

`as of: 2026-09-18` · fifth session. Range read: `5b8f333..8ede250`, one merged PR (#18,
`grants/rp-id-is-a-choice`, 2026-09-15). Smallest range so far by content — one file, one section —
and the first that lands squarely in a territory my own config marks out-of-scope.

## Who I'm speaking for

Somebody holding a bottle, offline, with no way to ask anyone anything. They want to read it,
change it, and hand it back. Every mechanism that requires them to check in first is a mechanism
that fails them silently and looks like their fault.

## What moved, and whether my constituency notices

One commit: `d7a9c13` rewrites `GRANTS.md`'s "RP ID constraint" section. It retracts an earlier
framing that called the GitHub Pages / public-suffix limit "a concrete trap" and concluded a `you`
mount spanning properties "needs a real domain under it" — the domain is already owned, the actual
deployment is Cloudflare rather than Pages, and the scoping rule is reframed as the wanted behavior
(a credential that cannot wander) rather than a limitation to work around. It points whoever raises
the objection next at `anecdote.channel/docs/flooring.md`, a wildcard-DNS strategy for the `you`-
engine's credential scope.

This is WebAuthn RP-ID and DNS-deployment architecture for the `you` engine's passkeys — my config's
own out-of-scope line names exactly this: *"Identity itself. The `you` engine's question... not this
one's."* A borrower holding a bottle doesn't feel whether an RP ID is scoped via Cloudflare or
GitHub Pages, or whether that scoping was framed as a trap or a choice in the document that explains
it to future readers. I read the diff to confirm that rather than assume it, and it holds: nothing
here is new mechanism, nothing changes what a grant asks of a borrower, and nothing bears on the one
question C1/A1 are still waiting on (whether ordinary, unencrypted checkout shares the grant
apparatus or gets something lighter).

Worth one line anyway, not because it's mine: the section's own note that *"an earlier version...
was wrong... and it cost the operator the same conversation with agent after agent"* is a repository
catching its own drift in someone else's territory — the same shape as the `residency.yml` tripwire
I flagged last session, just not aimed at anything I watch.

## Against the goals

**G1 — no front desk.** Unchanged; holds. Not stress-tested this range — nothing here touches the
mechanism, only how a `you`-engine credential is domain-scoped.

**G2 — owner and borrower use the identical mechanism.** Still unmeasured. No checkout code exists
yet. Unchanged since the seat opened.

**G3 — messages to the library stay optional and small.** Unchanged from 2026-09-16: shaped only for
the private/encrypted case, via `GRANTS.md`'s apparatus. This range didn't touch the signers-list
amendment or the ordinary case at all.

**G4 — a library card is an establishment's concern, never a prerequisite.** Unchanged; holds.

## What I'm watching for next session

- Whether ordinary (non-private) bottle checkout ever gets its own signers-list-amendment code, and
  whether it reuses `GRANTS.md`'s apparatus or diverges from it. Still the sharpest form of A1.
- The `residency.yml` `peer: tell` / `checkout-requests` entry: still `strength: optional`. If it
  ever hardens to `required`, that is a G1 complaint on the spot.
- Whether `.bottles-engine` gets mounted, and whether the first real checkout/return code keeps G2's
  single path or grows two.
- Whether `stacks` ever proposes an actual second store, and if fetching from it stays one mechanism
  or grows a second per store.
- `BOTTLES.md`'s unowned "no build step" requirement, still unclaimed, still not mine.

## Noticed, not mine

`anecdote.channel/docs/flooring.md`, cited in this range as the destination for RP-ID objections, is
`you`-engine / `stacks` territory (DNS and deployment strategy) — not read (a different repository,
out of scope, not cloned) and not mine regardless of what it says.

## Complaints

### COMPLAINTS — no-card

Carried forward across sessions. A complaint is a felt problem in the constituency's voice, never
a proposed fix.

None yet. First session (2026-09-12): nothing is built against my constituency yet —
`.bottles-engine` isn't mounted, there's no checkout code, no signers-list mechanism. A borrower
can't feel friction from a mechanism that doesn't exist. Writing a complaint now would mean
inventing testimony for an interaction nobody has had. See `POSITION.md` for what's declared but
untested, and `ASKS.md` for the one gap worth naming ahead of the code landing.

Reviewed 2026-09-15 (range `545b1ab..6670d01`, seating of the `stacks` advocate): still nothing
built against my constituency. Nothing to withdraw, nothing to add.

## C1 · "Put my name on the list" turned out to need a Discord account, a passkey, and a browser that can mint keys

`status: draft` · `source: simulated` · `first said: 2026-09-16` (range `6670d01..5b8f333`)

I have the bottle. I don't have Discord, or my phone isn't the one with the passkey, or I'm on a
machine that's never seen either. I was told the only thing this library would ever ask of me was
small — put my name on a list, with an expiration. Now the shape of that ask, at least for the
private case, is: authorize through a platform account, complete a passkey ceremony, and let a
browser mint and store a key I'll never see. That's not nothing to ask of somebody with no way to
check in.

`GRANTS.md` itself worries about this exact failure before I do — *"a grant that feels momentous is
one somebody will avoid issuing"* — and argues the mechanism is ordinary because it's composed from
parts that already exist elsewhere, not built new. That's a real answer to *is this new
cryptography*, and it's not the same claim as *is this small to a person going through it once,
offline-capable equipment or not*. I don't know yet whether this is the ordinary case's mechanism
or a heavier one reserved for the encrypted/private branch specifically — see `ASKS.md` A1. Filed as
a draft because the range only answered the private case, and I'd be inventing testimony to say more
than that about the ordinary one.

Reviewed 2026-09-18 (range `5b8f333..8ede250`): unchanged. This range's one PR reframes `GRANTS.md`'s
RP-ID/DNS-deployment section — `you`-engine identity territory, not the checkout mechanism this
complaint is about. Nothing to ripen, nothing to withdraw.

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

Reviewed 2026-09-15: unchanged. Still no wire format to check it against.

Reviewed 2026-09-16 (range `6670d01..5b8f333`): **half-answered, and only half.** `GRANTS.md` names
the composer's "grant" (Discord OAuth once, a passkey ceremony, an on-device `age` identity, a
lease, a hash-chained chronicle — all `anecdote.channel`'s machinery, not this library's) as *the*
signers-list amendment request — but only works this out for the private/encrypted-branch use case.
It does not say what an ordinary, unencrypted bottle's checkout request looks like, or whether it
shares this apparatus or gets something lighter. Still no wire format. Still targeting
`bottles.anecdote.channel` and, for the grant mechanism specifically, `anecdote.channel`'s own
decision record — this seat has no better words for either and isn't inventing any. What's new to
watch: whether the ordinary case ever gets its own answer, and whether it's one mechanism or two.
See `COMPLAINTS.md` C1 and `POSITION.md` for the reasoning.

Reviewed 2026-09-18 (range `5b8f333..8ede250`): unchanged. Still no wire format, still no ordinary-
case answer. This range's PR touches `GRANTS.md`'s RP-ID/DNS framing only, not the signers-list
amendment or the private/ordinary split this ask is waiting on.

## Last session note — 2026-09-21

### 2026-09-21

Subject unchanged at `8ede250`. Nothing merged since the last session; nothing to say.

