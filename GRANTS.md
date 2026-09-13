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
analogy it arrived in, and names the one derivation the design turns on.

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

## The derivation, and why the constitution forces exactly one answer

The operator flagged this as the open piece — *"how they derive that is still coming."* It is more
constrained than it looks, and the constraint is a good one.

**A passkey cannot decrypt anything.** A WebAuthn credential is non-extractable by design — the
`you`-engine brief already leans on this from the other side, noting *"passkey non-extractability
pushing the signing act into a browser gesture."* You can sign with it. You cannot hand its private
key to `age`.

That leaves two ways to get from a passkey to a decryption key:

1. **Authenticate to something that releases a wrapped key.** Sign a challenge, a service checks it,
   the service hands back your wrapped identity.
2. **Derive the key from the credential, on the device, with no network.** The WebAuthn **PRF
   extension** (`prf`, riding CTAP2's `hmac-secret`) returns a deterministic per-credential secret
   for a given salt, without ever exposing the credential's private key. That secret wraps the age
   identity.

**Option 1 is a front desk**, and [the README](README.md#no-library-card) refuses it in as many
words: *"Nothing central decides whether a change is allowed. A library that adjudicates has to be
online, trusted and correct, and this design refused all three."* A key-release endpoint is online,
trusted and correct, and its outage is your library going dark.

So **the no-library-card rule selects the mechanism.** Not a preference, not a benchmark — the
constitution admits one of the two options and it is PRF. That is a pleasing result and it should
be recorded as one, because it means the crypto decision was made years before anybody reached it.

    passkey (non-extractable, on the phone)
      └─ PRF(salt) ──▶ symmetric secret, derived on-device, offline
           └─ unwraps the age identity
                └─ decrypts the blocks on the library branch

Every step after the first is machinery this constellation already has: `age` throughout
`data-pile`, and `seal-enough` — *"the encryption factory, almost entirely WebCrypto-native"* —
whose one named gap is the age seed-wrap.

**What must be verified rather than assumed.** PRF availability is uneven across platforms and
authenticators, and this is precisely the kind of claim the store seat in
[`advocate.yml`](advocate.yml) is told to *measure rather than repeat* (G4). Treat it as the first
experiment, not as a settled capability. If PRF turns out to be unreachable on the phone that
matters, the fallback is **not** option 1 — it is a device-held identity minted the way
`age-mint.mjs` already mints one, with the passkey guarding the gesture rather than deriving the
key.

## The RP ID constraint, and a concrete trap in the worked case

The `you`-engine brief establishes that **the RP ID is exactly one decision, fixed at registration,
and not re-scopable afterward.** Two consequences that bear directly on the phone use case:

- **A credential is usable from any origin the RP ID is a registrable suffix of.** Created at
  `domain.com`, it works at `name.you.domain.com`. The reverse does not hold, and sibling labels
  cannot see each other's credentials.
- **An RP ID may not be a public suffix.** `github.io` is on the Public Suffix List, so a Pages site
  at `<user>.github.io` can only ever set RP ID to `<user>.github.io` — never `github.io`. **Two
  GitHub Pages projects under the same account cannot share a passkey.**

That last one is not hypothetical: it is the exact deployment of the first worked fitting, which is
served from Pages. **A `you` mount that is meant to span more than one property needs a real domain
under it**, and this is the cheapest possible moment to know that.

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
3. **The key travels with the person and is never fetched.** This is the rule the PRF choice
   enforces. *Walk up and read the thing without infrastructure* survives, because the reader brings
   their own key rather than asking for one.

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

Everything named already exists but one.

| engine | state today | what this design asks of it |
| --- | --- | --- |
| **library** | `draft` | the branch; enumeration and custody. `library.yml`, `PLACE`, the shelves |
| **data-pile** | **`running`** | the encrypted-at-rest branch store. **The load-bearing piece, and it was not on the operator's list** |
| **bottles** | `draft` | the transit object a grant-holder actually opens |
| **tell** | `running` | the door for people who hold nothing; [`OPEN.md` §4](OPEN.md) makes it the auth control point |
| **advocate** | `running` | the seats, including the store seat already studying this |
| **atlas** | `unstated` | routability. Still last |
| **`you`** | **does not exist** | RP ID, the PRF derivation, the grant. `notes/you-engine-brief.md` is a brief, and nothing is built |

**The gap is `you`, and it is now the keystone rather than an optional convenience.** That is a
change in its priority and the reason to write this down.

## Not decided here

- **Whether the grant expires, and what re-granting looks like.** The README's checkout carries an
  expiration; a Discord authorization has its own lifetime; a derived key has none. Three clocks, and
  nobody has reconciled them.
- **Whether PRF is reachable on the phone that matters.** The first experiment, per G4.
- **The RP-ID-versus-Tell collision.** [`OPEN.md` §4](OPEN.md) says the check belongs in
  `anecdote.channel/docs/decisions.md` and that nobody has run it. Still true, and now more urgent,
  because the grant makes it load-bearing rather than theoretical.
- **Revocation.** A key that has been derived once cannot be un-derived, and a grant-holder who has
  populated a local store keeps those bytes forever. This is the same boundary the worked fitting
  found at OPFS: *any withdrawal promise has a limit at the reader's disk.* It is a property of
  handing somebody bytes, not a defect to engineer away, and it should be stated to artists plainly
  rather than papered over.
- **What the branch move costs.** `station-node/docs/the-library-as-a-branch.md` staged it in five
  steps and step 1 is done; **step 2 is the remaining precondition** and it is in another
  repository. This document does not clear it.
