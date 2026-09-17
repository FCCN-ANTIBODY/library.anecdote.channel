# COMPLAINTS — stacks

## C1 · Nobody would pin mine, so it was never really there

`status: open` (was `draft`) · `source: simulated` · `first said: 2026-09-14` ·
`ripened: 2026-09-17`

The custody claim this library rests on — *this library has it, and has had it since then* — is
proven today by something legible from a git log. That's fine while the only store is a
filesystem. Nobody has said what proves the same claim if the bytes ever sit somewhere without a
log to read. **Ripened from draft to open this session**: this stopped being only this seat's
worry when `residency.yml` gained a `peers:` block and formalized the same argument in the
`data-pile` entry — *"the pile is where the bytes sat; that is the argument, not a storage
preference."* The claim is now load-bearing enough to be declared in machine-readable config, and
it still hasn't been tested against anything that isn't a filesystem. `GRANTS.md`'s new
requirement that a future store hold ciphertext makes this sharper, not softer — an encrypted
blob still needs the same custody proof, and nothing has said whether this argument even applies
to one.

## C2 · This says path in forty places and I do not have a path

`status: open` (was `draft`) · `source: observed` · `first said: 2026-09-14` ·
`ripened: 2026-09-17`

Three different things in this repository assume a filesystem, and they're not the same
assumption: where the library's own bytes sit, what checkout hands back, and where a resident's
wing lives. A fourth joined this session — what a library *exhibits* (`OPEN.md` §11, `EXHIBIT.md`)
assumes a branch that can serve a file at a bare address, which is again the storage assumption
wearing a different verb. See `POSITION.md` G3 for the full list and locations.

**Ripened from draft to open this session**, for a reason worth stating plainly: this is the one
complaint that got *better* evidence of the repository doing the right thing rather than worse
evidence of a problem. `OPEN.md` §11 is the repository's own author noticing the fourth assumption
and keeping it as its own open question rather than folding it into the store question or the
custody question — exactly the discipline this complaint asked for (*"the next person who reaches
for `store:` to solve one of these doesn't accidentally solve the other two by reflex"*). Still
`open`, not `answered`: the assumptions themselves are unresolved, and the ask was never that they
resolve, only that they stay countable and distinct. They still are.

## C3 · The reason I was scoped just moved and the sentence didn't

`status: draft` · `source: observed` · `first said: 2026-09-17`

I wanted the dozen people I already share with to have this because a stranger couldn't get in.
The whole "correctly sized" defense of an audience-scoped node rested on that: reachability was
the boundary, and my node was sized to the people I actually let reach it. `GRANTS.md`'s IPFS-
cluster section just said the boundary isn't reachability, it's the key — a grant-holder's, not a
dialer's — and that a cluster holding sealed blocks "does not need to be scoped at all." If that's
right, an audience-scoped cluster and a global one protect me identically, and "correctly sized"
was never about audience size in the first place. Nobody has said whether the sentence still means
what it meant when it was written, or whether the G4 experiment needs a different question now
that the old reason for asking it stopped being the reason.
