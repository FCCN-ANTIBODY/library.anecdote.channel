# COMPLAINTS — no-card

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
