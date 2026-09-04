# Open questions

`status: draft` — written 2026-09-03 while stubbing this repo. None of these is decided.

## 1. Does `library` subsume `bottles` as a subdomain concept?

**The observation that raises it:** every mechanic of checking a bottle out, writing to it, and
putting it back is **identical** whether the bottle sits under a `bottles` subdomain or a `library`
one. Who owns it and who may modify it are not special-cased anywhere. If the mechanics are the same,
two subdomain concepts may be one concept with two names.

**What argues against collapsing them.** A library is **not the same kind of diverse node** another
category is. `bottles.<apex>` is D4/D11's free-form cubby space — arbitrary origins, storage engines,
anything. A library is a curated, enumerating collection with an admission posture. Those are
different jobs even when the lending machinery is shared.

**What argues for it.** Having both a bottles engine and a library engine installed on one node —
say a Tell server — looks like two tools doing one job. A single tool would be a clearer path.

**Not resolvable from here.** It touches D4 (bottles topology) and D11 (storefront and intake), so it
is a constellation decision, not this repo's to take.

## 2. A library installed on someone else's node — what makes it discoverable?

A Tell server can run a library. But **a Tell registering with an Atlas means the Tell was
discovered — not that every tool on it is public.** Registration discovers the node, not its
contents.

So a library mounted on a node needs its own answer to *how does anyone learn this is here*, and that
answer must not accidentally publish the node's other tools. Unwritten.

## 3. Where does the `you` engine belong — the library, or the node running it?

Stated both ways in the same breath, and **the node is the better instinct.** A library does not
authenticate anybody (see the no-library-card section in the README); the thing a person authorizes
*against* is the node they are standing on. Mounting `.you-engine` here would imply an identity
relationship the design explicitly does not want.

The counter-case: if a library ever wants a voucher on a stable identity — not to gate reading, but
because it wants to know that the same masked person came back — the passkey a person already carries
is what it would want, and it has to reach it somehow.

**Leaning: the node mounts `.you-engine`; the library never does.** Not settled.

## Related, elsewhere

- **The control QR.** The `discoverywritten` work wants it for onboarding onto the bottle surface.
  The thought worth carrying: **it is more powerful if what you receive is a *library item* — which
  is a bottle — than a bare bottle.** An item arrives with provenance, a place it came from and
  something that enumerates it; a bare bottle arrives with none of that.
- **The signers-list amendment request** — the one message a borrower may need to send. No shape yet;
  must stay optional and stay small.
- `civic-node` `OPEN-QUESTIONS.md` §AA — the two layers of hooks, and loaning as a grant of write.
