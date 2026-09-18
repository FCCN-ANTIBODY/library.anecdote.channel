# POSITION — stacks

`as of: 2026-09-18` · subject `8ede250` · range `5b8f333..8ede250` (1 first-parent merge,
2026-09-15 — PR #18, `grants/rp-id-is-a-choice`).

**This range added nothing to any of the four goals below.** The merge's content — WebAuthn
RP-ID scoping to a domain suffix, and a DNS-wildcard deployment strategy for the `you` engine's
credentials — is identity/access architecture, not a claim about where bytes sit, how they're
proven held, or a filesystem assumption. What follows is carried forward unchanged from the read
of PRs #8–#17 on 2026-09-17; see that session's note, and 2026-09-18's, for why nothing moved.

## G1 · `store:` stays a word, not a driver layer

**Holding, and better tested than last session.** `residency.yml`'s `provides.store: filesystem`
is unchanged; no second value is implemented anywhere in the range. What's new is that other
authors in this range handled the temptation correctly without this seat having to say anything:
`GRANTS.md`, "The IPFS cluster question is already somebody's job," names this seat's G4 by id,
quotes the "run the experiment, do not quote the sentence" instruction verbatim, and explicitly
declines to choose IPFS — *"Nothing in this document changes that, and it should not be read as
choosing IPFS."* That is the discipline this seat exists to defend, exercised by someone else.
Recorded because it is evidence, not because it needed defending this time.

## G2 · Provenance outranks everything, and a second store must not change it

**Still unmeasured, and now cited from more places that all say the same thing.** The custody
claim — *this library has it, and has had it since then* — got a formal home this range:
`residency.yml` gained a `peers:` block, and its `data-pile` entry states the argument plainly:
*"Custody is checkable because the pile is where the bytes sat; that is the argument, not a
storage preference."* `without:` for that peer is *"bottles in a directory — they open, and
nothing about them is provable later."* That is the same git-native, filesystem-native claim
`OPEN.md` §5 already made — now load-bearing enough to be declared in a machine-readable peer
list rather than only argued in prose. Formalizing it did not test it: nothing here says whether
"the pile is where the bytes sat" still proves anything once the bytes don't sit anywhere a log
can read.

A second document adds a real constraint without answering this either. `GRANTS.md`'s IPFS-cluster
section — see G4 — concludes that any future store must **hold and address ciphertext**, because
"the privilege lives in the encryption rather than in the reachability." That's a new requirement
on top of G2's question, not a resolution of it: an encrypted blob still needs the same custody
proof a plaintext one does, and nothing has said whether "the pile is where the bytes sat" is even
askable about a blob nobody but the grant-holder can open.

## G3 · Name the filesystem assumptions, with locations — updated

**The repository did this seat's job for it once, which is the best possible outcome for G3.**
`OPEN.md` §11, "What does a library exhibit when it cannot serve a README?", raised — unprompted,
by `EXHIBIT.md`'s own author — exactly the class of finding this goal exists to produce:
`EXHIBIT.md` describes README-as-door as the general case, and §11 names the filesystem
assumption underneath it directly: *"`store:` in `residency.yml` already anticipates that a
second one might not be a filesystem at all. An IPFS-backed library plausibly has an index and
nothing that answers a request for `README.md`... `EXHIBIT.md` currently describes the filesystem
case and calls it the general one."* `EXHIBIT.md` itself carries the same admission in its own
"related, elsewhere" section. Adding this as a fourth item to the running list from last session:

1. **The bytes the library holds.** `RESIDENCY.md`, "The store is a variable." Unchanged this range.
2. **Checkout, separately from storage.** `BOTTLES.md` §1.4. Unchanged this range.
3. **Where a resident lives.** `RESIDENCY.md`, wing mechanism. Unchanged this range.
4. **What a library exhibits.** `EXHIBIT.md` / `OPEN.md` §11, new this range. README-as-index
   assumes a branch that can serve a file at a bare address; an IPFS-backed library may have
   nothing to serve but a bottle to open. `OPEN.md` §11 sketches three ways this could land and
   resolves none of them — correctly, since it says the answer needs a branch-fragment build that
   doesn't exist yet.

`SHELVES.md` (new this range) is a fifth filesystem-shaped decision — `share/` and `build/` as
top-level prefixes, justified explicitly as filesystem precedent (*"the precedent is the
filesystem's"*) — but it's named out loud as borrowed idiom rather than assumed silently, so it
isn't added as its own item; it's the same case as (1), stated with unusual honesty about where
the metaphor comes from.

## G4 · Measure the "correctly-sized" claim, don't repeat it

**Still no experiment run. The question the experiment would answer moved, though, and that's
worth recording.** `GRANTS.md`'s IPFS-cluster section reframes what "correctly sized" was ever
resting on: the original claim scoped a node to *who could reach it*. GRANTS' finding — privilege
lives in encryption, not reachability — means *"a cluster holding sealed blocks does not need to
be scoped at all."* If that holds, the audience-scoping story this claim was built to defend may
not be the thing doing the work anymore, and nobody has said whether "correctly sized" still means
what it meant when the sentence was written. Not treating this as an answer — it's a change in
what would need measuring, not a measurement. See complaint C3.

Separately, `adoption/worked/artist-lockers.md` (a fitting of an unrelated third-party project)
describes a real, observed IPFS-via-Pinata-gateway architecture — durable bytes needing a CID,
a CID needing a gateway to resolve. That's real evidence about how IPFS access actually behaves
under load, but it answers a different question (media durability against link rot for a public
Discord catalogue) than this seat's (an audience-scoped node for people already being shared
with). Noted as material that could inform a future experiment, not as the experiment run.
