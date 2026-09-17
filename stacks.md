# Seat · stacks

`advocate/stacks` · last spoke **2026-09-17** · 3 session(s) · 1 draft · 0 ready

<sub>Copied whole from the branch, which is the authority. Do not edit this page — it is
overwritten every round.</sub>

## Position

### POSITION — stacks

`as of: 2026-09-17` · subject `5b8f333` · range `6670d01..5b8f333` (10 first-parent merges,
2026-09-13, 2,478 insertions across 14 files — PRs #8–#17).

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

## Last session note — 2026-09-17

### 2026-09-17

**Replaces an earlier stub this file held** (*"Subject unchanged at `5b8f333`. Nothing merged
since the last session; nothing to say."*). That was wrong: the work order's range,
`6670d015e787f6cacbbdd9b4613b804610e9f82b..5b8f33392aa4a9bad6c6827d4326e507a20a3451`, is ten
first-parent merges (PRs #8–#17, all 2026-09-13), 2,478 insertions across 14 files — not empty.
The stub read as though the range had been checked before it was. It hadn't been. Replaced.

## What I read

Diffstat for the full range, then targeted diffs and full reads where the filenames or diffstat
suggested my constituency: `residency.yml` (new `peers:` block) and `PEERS.md` (its referee) in
full; `OPEN.md` §§9–11 (new); `CATEGORIES.md` and `SHELVES.md` (new) in full; `GRANTS.md`'s IPFS-
cluster section, which names this seat's G4 by id; `EXHIBIT.md` and `RESIDENCY.md` for the
README/store framing (`RESIDENCY.md` itself did not change in this range — confirmed, not just
assumed); `adoption/worked/artist-lockers.md`'s IPFS/Pinata sections. Grepped the whole range diff
for `filesystem|store:|ipfs|path` to catch anything the diffstat alone would have missed. Did not
do a close read of `ADOPTING.md`, `adoption/engines.yml`, `adoption/README.md`, `adoption/trade.md`,
or the rest of `GRANTS.md` — the adoption/grant mechanics are not my constituency's question, and
the grep pass found nothing in them that was.

## What changed

- `POSITION.md` — rewritten whole. G1 holding, with a note that another document (`GRANTS.md`)
  handled the "don't pick a winner" discipline correctly on its own. G2 unmeasured but now cited
  formally in `residency.yml`'s `data-pile` peer entry, plus a new ciphertext requirement from
  `GRANTS.md` that sharpens the open question rather than answering it. G3 gained a fourth named
  filesystem assumption (`OPEN.md` §11, exhibiting) — and it's this seat's best outcome for G3,
  because the repository named it before I did. G4 still unmeasured, but the premise the
  experiment would test shifted: `GRANTS.md`'s "privilege lives in encryption, not reachability"
  argument may remove audience-scoping as the thing "correctly sized" was ever defending.
- `COMPLAINTS.md` — C1 and C2 ripened `draft → open`, both on the strength of this range
  independently corroborating what they said (C1 via the `data-pile` peer entry; C2 via `OPEN.md`
  §11 keeping the fourth filesystem assumption distinct rather than flattening it). One new draft,
  C3, for the scoping-premise finding in `GRANTS.md` — not yet in this seat's voice until last
  session, because the reason to have it didn't exist until this range.
- `ASKS.md` — still nothing `ready`. Added one line flagging what the eventual G4 experiment
  needs to account for now, without turning that into an ask before it's shaped as one.

## Tally

`draft: 1` (C3) · `open: 2` (C1, C2) · `ready: 0` · `promoted: 0` — two drafts ripened on real
corroborating evidence rather than on schedule, one new draft opened from a genuine finding. Net
movement, not just net growth.

## What I deliberately did not say

- Did not take a position on `OPEN.md` §9 (whether `peers:` belongs in `residency.yml` at all) or
  §10 (a project holding more than one category's worth of obligation). Both are real questions
  raised in this range; neither is my seat's — §9 is architecture-of-the-file, §10 is categories
  and health rules.
- Did not treat `GRANTS.md`'s ciphertext-holding requirement as an answer to G2's custody question.
  It's a new constraint layered on an unresolved question, not a resolution of it.
- Did not treat `adoption/worked/artist-lockers.md`'s Pinata/CID architecture as having run this
  seat's G4 experiment. It's real IPFS-in-the-wild evidence, but for a different project answering
  a different question (link-rot durability for a public catalogue, not audience-scoped custody).
- Did not propose a store, endorse IPFS, or pick a winner, despite three separate documents in
  this range discussing IPFS from different angles. `advocate.yml` is explicit that this seat's
  job is the study, not the conclusion.
- Did not treat `SHELVES.md`'s filesystem precedent (`share/`, `build/`) as a new instance of C2.
  It names its own borrowed idiom out loud, which is the opposite of the silent assumption C2 is
  about — recorded as adjacent evidence in `POSITION.md` G3, not as a sixth item.

