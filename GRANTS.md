# Grants — what makes a local copy a privilege

`status: draft` — written 2026-09-13, from the operator's decision to read the library branch as
the git-side equivalent of the browser's origin-private filesystem:

> *"We should conceive of a library with branch functionality, which is to say keeping the library
> on a branch instead of on a file prefix on the main branch, where the implementation is OPFS…
> the use case is that someone would be on their phone and have a passkey… we can secure a
> trustworthy grant by authorizing you to your Discord account there and continue to show you
> trusted stuff that normally Discord might expire. And so saving them to your local storage is a
> sign of privilege here."*

**Nothing has moved.** This document answers a question that was already open, corrects the
analogy it arrived in, and — after a first draft that designed before it checked — points at the
machinery that already implements the answer.

## The mood: a grant is a delegation of capability, and that is all

`Added 2026-09-13`, from the first adopter reading this document. **This section is about tone, and
tone is load-bearing here**, because everything below it is easier to misread than to read.

The adopter had the word already — their own OAuth exchange sends
`grant_type: "authorization_code"` — and asked whether ours was the same word. **It is the same
word, and theirs is the plainer sense.** The operator's answer, and the reading this repository
prefers:

> A grant is **a delegation of capability**. Not a superuser, not an elevation, not a tier of
> access somebody is promoted into. It *can* be built up until it elevates that much, but that is
> not the mood it is delivered in.

So the default picture is the ordinary one: **somebody may now do a specific thing, usually narrow,
usually with an expiry, and usually because they asked politely once.** OAuth is where most people
meet the word and OAuth is not a superuser system. Neither is this.

### Why the mood is worth a section

Two failures, and both are the kind that arrive quietly:

- **An adopter who reads *privilege* as *admin* concludes that adopting grants means building an
  authorization system**, and correctly declines, because they do not have one and do not want one.
  The truth is nearer the opposite: a grant exists so that *nothing* has to adjudicate.
- **A designer who reads *privilege* as *rare and heavy* builds a ceremony around it.** The design
  wants grants to be common, cheap, and boring. A grant that feels momentous is one somebody will
  avoid issuing, and a capability nobody delegates is a capability that stays centralised.

### What the title of this document means, then

**This document's *privilege* names a consequence in one use case, not the definition of the word.**
The case is specific — a local copy that outlives Discord's clock — and *that* copy is a privilege in
the ordinary English sense: a nice thing not everybody has. It is not a claim that grants are a
permissions ladder.

The refusals elsewhere in this repository already enforce the light reading, and they are the reason
it can be trusted rather than merely asserted:

- **No front desk**, so there is nothing for a grant to be *above*.
- **No library card**, so a grant cannot become a prerequisite to reading.
- **The key travels with the person**, so a grant-holder asks nobody at the moment of use.

A grant that required a superuser would need somebody to *be* super. There is deliberately nobody.

### Where the word came from here, and it was not us

**The adopter's project predates all of this.** They were using `grant` in its ordinary sense before
this constellation existed, and the convergence is a point in the word's favour rather than
something they need to reconcile to. Recorded because the opposite framing — *our term of art, which
you now also use* — would be both wrong and the sort of thing that makes onboarding feel like
assimilation.

## What this settles

[`OPEN.md` §3](OPEN.md) ended on a hinge and said so:

> *So: **the `you` engine is not required — unless it is the way a grant to take something out of
> the library is understood.** That is the whole hinge, and it is now the only version of this
> question worth asking.*

**It is the way a grant is understood.** That is the answer, and it arrived as a use case rather
than as a ruling, which is the better way for it to arrive. The `you` engine moves from *optional,
leaning against* to **the keystone of holding** — because without it there is no way to say that
this person may read these bytes, and *holding* rather than *pointing* is the library's whole
distinguishing claim.

§3's lean — *the node mounts `.you-engine`; the library never does* — survives intact. The library
still authenticates nobody. It holds ciphertext and hands it to anyone who asks. What the grant
changes is not who may **fetch**, it is who may **read**, and that distinction is the entire design.

## The correction: a branch is not OPFS

The analogy is productive and it is wrong in the one place it is load-bearing. Worth being exact,
because [`SHELVES.md`](SHELVES.md) and `station-node/docs/the-library-as-a-branch.md` both already
say *private by default*, and that phrase will be misread by somebody eventually.

| | OPFS | a git branch |
| --- | --- | --- |
| scoped to | one origin | the repository |
| listable from outside | **no** — nothing can ask your browser what it holds | **yes** — `git ls-remote` shows every branch to any reader |
| obtained by default | no — bytes arrive because you fetched them | **yes** — `git clone` takes all of `refs/heads/*` |
| exportable | **no** (the finding in [`adoption/worked/artist-lockers.md`](adoption/worked/artist-lockers.md)) | yes; that is what a branch is |
| survives the device | no | yes |

So a branch gives **isolation** — the airlock property, real and worth having: *content not on the
branch a build reads cannot be published by mistake*. It does not give **privacy**. On a public
repository, `git fetch origin library` is available to everybody, and a plain branch cannot carry
the sentence *saving them to your local storage is a sign of privilege*, because no privilege was
required to get them.

**A refinement worth knowing and not sufficient by itself:** content can live under a custom ref
namespace — `refs/library/*` rather than `refs/heads/*` — which is not fetched by a default clone
and not shown by `git branch -r`. That is how Gerrit carries `refs/changes/*` and how `git notes`
stays out of the way. It buys *you only have it if you asked for it*, which is genuinely one of
OPFS's properties. It is obscurity, not confidentiality, and should never be described as the
latter.

## What actually makes it a privilege, and it is already running

The property the analogy wants exists in this constellation today, in
[`data-pile`](https://github.com/FCCN-ANTIBODY/data-pile), whose maturity in
[`adoption/engines.yml`](adoption/engines.yml) is `running`:

> *Fork it, deploy it (a **public** repo is the intended default), and only you can read what it
> holds — until you choose to prove it to everyone.*

A **public** repository, an append-only encrypted log, on **its own branch** (`feed/tell`), readable
by nobody without the key. That is a solved instance of exactly this problem, shipped, with a
custody-proof story attached. It is also already declared as a peer of this engine for `custody`.

So the shape is not *branch = OPFS*. It is:

> **The branch is the isolation. The encryption is the privilege. The grant is the key.**

Three separable things, and conflating any two of them is how this gets built wrong. The branch
keeps other people's builds from touching it. The ciphertext makes fetching it useless. The grant is
what turns a fetched blob into something you can open.

## The derivation: compose what is built, and let the invariant explain why

The operator flagged this as the open piece — *"how they derive that is still coming."* It is more
constrained than it looks, and it is **already built**, which the first draft of this document
missed by designing before checking the demo shelf.

### The invariant got there first

**A passkey cannot decrypt anything.** A WebAuthn credential is non-extractable by design; you can
sign with it, and you cannot hand its private key to `age`. That is a mechanical fact about
WebAuthn — and the constellation had already ruled it as law, years before anybody walked into it
from this direction:

> **Invariant 4. Sign ≠ decrypt.** *Signing is public authorship/integrity; encryption controls
> reading. Keep them separate.*

So the question *"how does the passkey decrypt the library"* is malformed, and the invariant says
why. **The passkey does not decrypt. It gates.** Everything below follows from taking that
seriously rather than from any cryptographic cleverness.

### The pattern is on the demo shelf

`anecdote.channel/AGENTS.md`, under *"You are the second factor"*:

> Signing happens **here, on the device**: WebCrypto Ed25519 under a non-extractable key in
> domain-scoped IndexedDB, **gesture-gated by a passkey ceremony** (`composer/sign.mjs`,
> `composer/gesture.mjs`).

The key lives on the device. The passkey proves a person is present at the moment it is used. Two
separate things, exactly as invariant 4 requires, and `composer/gesture-demo.html` is the shipped
proof of it.

The rest of the chain is likewise already sitting there:

| need | what already exists |
| --- | --- |
| an identity that can decrypt | `composer/age-mint.mjs` — a browser-minted `age` identity, byte-interoperable |
| a place to keep it that is not a server | domain-scoped IndexedDB, non-extractable, per `sign.mjs` |
| proof a person authorized this use | the passkey ceremony, `composer/gesture.mjs` |
| **the grant itself** | **`composer/grants-panel-demo.html`** — *"Running on your behalf": mint / touch / revoke standing consent grants, each row showing the artifact that proves it* |
| an expiry that can be refreshed | `composer/lease.mjs`, the freshness lease |

    passkey ceremony  ──gates──▶  age identity (minted on-device, held in IndexedDB)
                                        └─ decrypts the blocks on the library branch
    grant artifact (mint/touch/revoke) ──says which blocks, and until when

**Nothing in that line is new.** It composes `age-mint`, `gesture`, `lease` and the grants panel,
which is what *"if the need category is represented, the machinery exists — compose it, don't
rebuild it"* asks for.

### What this replaces, and why the replaced version was wrong

An earlier draft of this document argued that the no-library-card rule forces the **WebAuthn PRF
extension** (`prf`, over CTAP2 `hmac-secret`) — deriving a wrapping key from the credential rather
than storing one. The reasoning was that the only alternative was a key-release service, which is a
front desk.

**The conclusion was right and the mechanism was wrong.** No key-release service, correct. But
storing a device-held `age` identity is the *other* way to avoid one, it fetches nothing, and it is
built. PRF was new dependency surface proposed in front of a shipped answer — and it runs at
invariant 8, *"no new cryptography without cause: WebCrypto Ed25519, `age`, `sha256`. Every
capability here was built by composing these."* PRF is not in that set.

**Where PRF might still earn its cause, stated so nobody has to re-derive it:** an IndexedDB
identity is per-origin, per-device and evictable — lose the profile and the grant is gone, and a
second device needs a second minting. A PRF-derived key regenerates from a passkey that syncs
through the platform keychain, so it would survive both. That is a real advantage and it is a
**portability** argument, not a security one. It belongs in `anecdote.channel/docs/decisions.md` as
a cause to weigh if device loss becomes the complaint, and nowhere near the first build.


## The RP ID is a choice this constellation makes, not a ceiling it hits

The `you`-engine brief establishes that **the RP ID is exactly one decision, fixed at registration,
and not re-scopable afterward.** That decide-once-ness is real and it is the part worth carrying:

- **A credential is usable from any origin the RP ID is a registrable suffix of.** Created at
  `domain.com`, it works at `name.you.domain.com`. The reverse does not hold, and sibling labels
  cannot see each other's credentials.
- **An RP ID may not be a public suffix.** `github.io` is on the Public Suffix List, so a Pages site
  at `<user>.github.io` can only ever set RP ID to `<user>.github.io` — never `github.io`.

### Do not raise this as an objection to our deployment

**An earlier version of this section did, and it was wrong to.** It presented the `github.io` case
as *"a concrete trap in the worked case"* and concluded that a `you` mount spanning properties
*"needs a real domain under it."* The facts are accurate; the framing has cost the operator the same
conversation with agent after agent, because this was the only mention of the Public Suffix List
anywhere in the constellation and reading it primed the objection.

Three corrections, and the third is the one that matters:

1. **GitHub Pages is not the deployment.** Cloudflare is. Where a Pages site still appears it is a
   demonstration that something works *without a worker*, not the architecture.
2. **The domain is ours**, so the suffix question was always a choice rather than a ceiling. The
   sentence *"needs a real domain under it"* described a requirement that was already met.
3. **Breadth is not what is wanted, and the scoping rule delivers the requirement.** The objection
   assumes an attempt to make one credential span properties. For a floor, the goal is the
   opposite — a credential that is *only for this one thing* — so a rule that prevents a credential
   from wandering is the feature. And scope is already a configuration rather than a constraint:
   **D9** records that `composer/gesture.mjs` parameterizes rpId, and **D12** settles which scope
   was chosen and why.

**The strategy has a name now: see `anecdote.channel/docs/flooring.md`.** One identical page served
at every label under a wildcard, nothing provisioned ever, the label chosen rather than allocated —
which is this library's own *no front desk* rule expressed in DNS. That document is the destination
for this objection, and it is written to be found by whoever is about to raise it.

What survives here, unchanged, is only the decide-once-ness: an RP ID is baked into a credential at
creation, so **it is settled before the first enrolment or it is settled by re-enrolling everybody.**
That is a fact about WebAuthn and it is not an argument against anything we are doing.

## Why a grant is not a library card

The obvious objection, and the README answers it before it is raised. The *one* sanctioned reason to
talk to a library is already this:

> *The only real reason to talk to a library is to ask for a specific checkout — **put my name on
> the signers, with an expiration.** A request to amend a list, not an authentication.*

A grant **is** that request. Discord authorization establishes, once, that you are entitled; the
result is your name on a signers list carried by the artifact, with an expiration. Nothing is
consulted at read time.

Three properties keep it on the right side of the line, and losing any one of them turns it into a
card:

1. **The check is against the artifact, never against a service.** A bottle's signer list is in the
   bottle. The library is not asked.
2. **Ciphertext does not adjudicate.** A blob that fails to decrypt has not refused you; there is no
   decision, no decider, and nothing to be online.
3. **The key travels with the person and is never fetched.** This is what minting on-device buys,
   and it is the property that made a key-release service unacceptable. *Walk up and read the thing
   without infrastructure* survives, because the reader brings their own key rather than asking for
   one.

The README's *"an artifact must remain openable by somebody who never authenticated"* is not
violated by encryption — it is a rule about **not requiring infrastructure**, not a rule that
everything is plaintext. What it forbids is a reader who must ask permission at the moment of
reading. A reader holding their own key asks nobody.

## What this makes of the worked case

[`adoption/worked/artist-lockers.md`](adoption/worked/artist-lockers.md) found that the project's
Discord auth gate is cosmetic by construction: every reference ships inside the static HTML before
the overlay is drawn, and **a static host cannot gate, it can only decorate.** That was recorded as
a structural fact with no remedy.

This design is the remedy, and it works by giving up on gating:

> **Serve the ciphertext.** A static host that cannot gate does not need to, because the bytes it
> serves to everyone are readable only by the grant-holders. The gate stops being a lie and becomes
> unnecessary.

It also answers their actual pain in their own terms. Discord CDN URLs expire — `bot/cdn.py` knows
precisely when. A grant-holder's local store is populated with **bytes**, not links, so it outlives
Discord's clock; and Discord OAuth is demoted from *the thing that serves you the media* to *the
thing that established, once, that you were entitled to it.* That is the operator's sentence —
*continue to show you trusted stuff that normally Discord might expire* — with the mechanism under
it.

Their `acquireBlob()` already has the tier structure this needs.

## The IPFS cluster question is already somebody's job

*"What we are considering is becoming our own IPFS cluster"* is not a new question here — it is
goal **G4** of the store seat in [`advocate.yml`](advocate.yml), monthly cadence, phrased as a claim
with an experiment attached:

> *"An IPFS node scoped to the audience a library already exposes itself to is not a degraded global
> store, it is a correctly sized one" is a claim with an experiment behind it. **Run the experiment;
> do not quote the sentence.***

The seat is also explicitly forbidden from picking a winner — *"IPFS is this seat's first study, not
its conclusion."* Nothing in this document changes that, and it should not be read as choosing IPFS.
What it does add is a **requirement** the seat did not have: whatever the second store turns out to
be, it has to hold ciphertext and address it, because the privilege lives in the encryption rather
than in the reachability. A cluster scoped to an audience is a smaller version of *fire it out
there*; a cluster holding sealed blocks does not need to be scoped at all.

## Where this leaves the engines

**Not restated here.** The roster is [`ADOPTING.md`](ADOPTING.md) for people and
[`adoption/engines.yml`](adoption/engines.yml) for agents, both with per-row provenance, and a third
copy in this file would be a fact that can disagree with two others.

Only what is new is recorded, which is one thing:

- **`you` is not on the roster, because it cannot be adopted.** There is no repository — only
  `notes/you-engine-brief.md`, which is a relayed brief with nothing built. What this document
  changes is its *standing*: it moves from an optional convenience to the piece that holding turns
  on. It should stay off the roster until it exists, because a roster row is an offer.
- **The engine the design actually leans on was not on the operator's list**: `data-pile`, already
  `running`, already declared a peer of this library for `custody`.


## The vernacular, and the one home it has to end up in

**Ruled 2026-09-13: the composer's grant and the library's grant are one concept.** The operator's
answer to the question this document opened — *"yes, I believe they are the same concept. Library
has sharpened thinking for how to make use and find best vernacular."*

So the mechanism is `anecdote.channel`'s, because that is where the artifact is built
(`composer/grants-panel-demo.html`, `composer/lease.mjs`, `composer/authorize.mjs`) and because
capability moves there. **The vocabulary is mostly there too** — more of it than this document first
assumed, which is recorded below rather than quietly corrected.

[`BOTTLES.md`](BOTTLES.md) already settled how that resolves, and its reasoning transfers without
amendment:

> **The table is not reproduced here**, and resisting the urge to leave a convenience copy is the
> point: two homes for one fact is the failure this constellation keeps naming.

**So this section is temporary by construction.** The one thing the library does add is *offered*,
not asserted — carried here only until `anecdote.channel` takes it or refines it, and **deleted the
day it lands there**, exactly as `bag` / `bottled` / `canonical` were deleted from `BOTTLES.md`. It
is the prose form of what [`adoption/engines.yml`](adoption/engines.yml) calls
`declared: transcribed` — *a debt with a name, and a small owed pull request.*

### Most of the vocabulary already exists, and it is not the library's

Checked before claiming anything, because the first draft of this document was wrong in exactly this
way. `anecdote.channel` has thought about grants considerably harder than the table this section
originally carried gave it credit for. Already named there, and **not restated here**:

- **scope** — a grant is `{piles:[<name>]}`, bound at the hello to the browser-attested asking origin
- **session-lived versus standing** — two lifetimes, with *"standing grants come via the grants panel"*
- **the ladder**, **`grantId`**, and the **chronicle** — every vend appended to a hash-chained local
  log, so an act that skipped the ceremony is absent from it
- **consent as a platform gesture at an authority boundary, never web-painted** — `docs/consent-surface.md`
- revocation as `port.close()`, and gesture-gating throughout

Cite those. The library did not invent them and has no better words for them.

### What the library actually adds, which is narrow

One thing, and it is a **mode** rather than a word:

> **A grant that must be exercised with no keeper in reach.**

Every grant in `anecdote.channel`'s model is vended: something is asked, at a boundary, and the act
is chronicled. The library refuses that shape by constitution — *no front desk*, nothing central
deciding, nothing that has to be up. So the library's instance of the concept runs in a mode the
existing vocabulary does not yet cover: **the reader already holds the ciphertext and the key, and
opens it with nothing to ask and nothing watching.**

Two consequences fall straight out, and both are the library's to report rather than to decide:

| | in the vended mode | in the keeperless mode |
| --- | --- | --- |
| what the grant governs | an **action** at a boundary — vend, sign, access a pile | **reading** bytes already in hand. Fetching is never gated |
| the chronicle | every vend is logged | **a read cannot be chronicled.** There is nothing present to append to a log, and adding something would be the front desk arriving by the back door |

The second is the uncomfortable one and it should be said plainly rather than discovered: *every use
of your identity is auditable* has a boundary, and the library is where it stops.

### The one consequence this library must not forget

`BOTTLES.md` keeps exactly one thing back from the vocabulary it gave away — the consequence the
library is *positioned to break*. The equivalent here:

> **A grant may never become a prerequisite for opening an artifact.** It governs who may **read**
> what is held; it never governs who may **fetch**, and it is never consulted at the moment of
> reading.

The library is the party that would benefit from forgetting this, because a library that can gate
looks more capable than one that cannot. That is exactly why it is written on the library's side of
the line and not the composer's.

## Not decided here

- **Which clock governs, now that two of the three turned out to be one.** The composer's lease
  *is* the README's expiration, so re-granting is `touch` and there was never a second mechanism to
  design. What is genuinely unreconciled is the third: a Discord authorization has its own lifetime,
  set by somebody else, and nothing says what happens to a grant when the authorization behind it
  lapses.
- **The RP-ID-versus-Tell collision.** [`OPEN.md` §4](OPEN.md) says the check belongs in
  `anecdote.channel/docs/decisions.md` and that nobody has run it. Still true, and now more urgent,
  because the grant makes it load-bearing rather than theoretical.
- **Revocation, which is narrower than it looked.** The grants panel already mints, touches and
  **revokes**, so revoking the grant is a solved gesture rather than an open problem. What remains
  open is only the floor beneath it: a grant-holder who has already decrypted keeps those bytes
  forever. This is the same boundary the worked fitting
  found at OPFS: *any withdrawal promise has a limit at the reader's disk.* It is a property of
  handing somebody bytes, not a defect to engineer away, and it should be stated to artists plainly
  rather than papered over.
- **What the branch move costs.** `station-node/docs/the-library-as-a-branch.md` staged it in five
  steps and step 1 is done; **step 2 is the remaining precondition** and it is in another
  repository. This document does not clear it.
