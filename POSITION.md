# POSITION — no-card

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
