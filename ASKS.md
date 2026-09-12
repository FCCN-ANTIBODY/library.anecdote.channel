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
