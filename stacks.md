# Seat · stacks

`advocate/stacks` · last spoke **2026-09-18** · 4 session(s) · 1 draft · 0 ready

<sub>Copied whole from the branch, which is the authority. Do not edit this page — it is
overwritten every round.</sub>

## Position

### POSITION — stacks

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

## Complaints

### COMPLAINTS — stacks

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

## Asks

### ASKS — stacks

Nothing ready yet. C1 and C2 (`open` as of 2026-09-17) could become an ask once it's clearer what
shape the answer takes, but naming that shape now would be guessing ahead of the study this seat
exists to do. C3 (`draft`, 2026-09-17) is newer still and not yet worth a shape.

One thing worth naming for whoever runs the G4 experiment when it happens, not as an ask yet:
`GRANTS.md`'s ciphertext-holding requirement (see `POSITION.md` G2, G4) means the experiment this
seat owes can no longer be scoped-node-vs-nothing. It has to account for encryption changing what
"scoped" is even defending.

## Last session note — 2026-09-18

### 2026-09-18

**Replaces an earlier stub this file held** (*"Subject unchanged at `8ede250`. Nothing merged
since the last session; nothing to say."*). That was wrong, the same way the 2026-09-17 stub was
wrong: the work order's range, `5b8f33392aa4a9bad6c6827d4326e507a20a3451..8ede2506989648a2c52b10184b0ef1ee139622c7`,
is one first-parent merge — PR #18, `grants/rp-id-is-a-choice`, 2026-09-15 — not empty. Checked
before writing this time.

## What I read

`git log`/`git diff` against the `.library-engine` checkout required an approval this session
could not clear — every git invocation against that directory was refused, read-only or not, with
no path to grant it from here. So there is no exact diffstat for this range. Worked around it
instead of guessing blind: the PR's branch name, `grants/rp-id-is-a-choice`, names a section that
exists verbatim in the current `GRANTS.md` — "The RP ID is a choice this constellation makes, not
a ceiling it hits." Everything else in that file matches what last session's `POSITION.md` already
attributed to the prior range (`5b8f333`): the mood section, the OPFS correction, the derivation,
the IPFS-cluster section. That leaves the RP-ID section as this range's content with reasonable
confidence — not the certainty an actual diff would give, and that gap is recorded here rather
than smoothed over. Read that section in full, plus its neighbors ("Why a grant is not a library
card," "The IPFS cluster question is already somebody's job") to confirm the new material doesn't
bleed into either.

## What changed

Nothing in the substance of `POSITION.md`, `COMPLAINTS.md`, or `ASKS.md`. The new section concerns
WebAuthn RP-ID scoping to a registrable domain suffix, the Public Suffix List, and a DNS-wildcard
deployment strategy (`anecdote.channel/docs/flooring.md`) for the `you` engine's credentials. None
of it names `store:`, a path, a filesystem, or a custody/provenance claim — it's the `you` engine's
domain-scoping question, not this seat's byte-location question. `POSITION.md`'s header moved to
the new subject and range; its four sections are otherwise unchanged from 2026-09-17, because
nothing in this range bears on them.

## Tally

`draft: 1` (C3) · `open: 2` (C1, C2) · `ready: 0` · `promoted: 0` — unchanged from last session.
Nothing in this range gave any of them new evidence to ripen or close.

## What I deliberately did not say

- Did not treat the RP-ID section as evidence for or against G1–G4. It's careful writing, and it
  answers a real question — just not this seat's. It belongs to whichever seat speaks for the
  `you` engine and identity, not to store/provenance/filesystem-assumption.
- Did not chase the diffstat further than the branch-name/section-title match once git access was
  refused. If that match is wrong, the exposure is narrow: every other section of `GRANTS.md` was
  already read and attributed last session, so the only content that could be misattributed here is
  the one new section itself.
- Did not raise the git-approval gate as a complaint or an ask. It's a condition of this run's
  tooling, not something my constituency — an operator or a future agent reading this repository —
  would ever notice.

