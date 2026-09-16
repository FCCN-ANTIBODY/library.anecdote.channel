# ASKS — no-card

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
