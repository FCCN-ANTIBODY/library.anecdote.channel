# Open questions

`status: draft` — written 2026-09-03 while stubbing this repo. None of these is decided.

> **Narrowed 2026-09-03.** §1 and §2 below turned out to be one question wearing two hats:
> **how does a Tell server with a library talk about the content on it?** Everything is isolated
> today; the open part is what it means for it *not* to be. The sharpening is in §2.

## 1. Does `library` subsume `bottles` as a subdomain concept?

> **Answered from outside, 2026-09-08 — and not by this repository.** The operator asked for
> `bottles.anecdote.channel` back **as a repository, by name**, and for the material to be divided
> that way. So the answer is *no, they do not collapse*, and the reasoning below that argued against
> collapsing is the reasoning that held.
>
> **This repo did not take the decision and is not recording one.** It touches D4 and D11, so the
> decision record is still owed in `anecdote.channel/docs/decisions.md`, and until it is written
> this note is a report of what the operator wants rather than a constellation fact. What changed
> here is only that this repository stopped waiting on it: see [`BOTTLES.md`](BOTTLES.md), which is
> written as a consumer's requirements precisely because the format is somebody else's to own.
>
> Carried in: `unplaced/bring-back-the-bottles-repository.md` on the node's petition ground.

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
is a constellation decision, not this repo's to take. That remains true; the note above is a decision
arriving, not this repository making one.

### What is still open inside it

**Who owns the player.** Both petitions flagged this as their own weakest boundary and neither
resolved it. The wire format clearly wants to be `bottles`; the **clean-room viewer** — a `data:`
origin with no network, no cookies, no ambient credentials, capable of carrying a bottle's own UI —
looks equally like `anecdote.channel`'s, as the static-system owner.

The library has no stake in which, and one real stake in the question being *answered*: it is the
piece the library depends on and cannot build. Recorded in [`BOTTLES.md`](BOTTLES.md) §1.2 as a
requirement with no owner.

## 2. A library installed on someone else's node — what makes it discoverable?

A Tell server can run a library. But **a Tell registering with an Atlas means the Tell was
discovered — not that every tool on it is public.** Registration discovers the node, not its
contents.

### The candidate answer: the Atlas is the UI

If a Tell registers, you know the repository where its library is kept. If that library's contents
are public, **the Atlas can enumerate them**, the same way it already categorises polls and
everything else. Which produces a genuinely simplifying possibility:

> **The library may not need a bespoke UI at all.** The Atlas is the directory. A library on a Tell
> probably still *has* one — it is a side system with its own surface — but it should not have to.

That is the strongest argument yet that a library is a kind and not an application: its whole job is
enumeration, and something upstream already enumerates.

### The constraint that stops it being automatic

**A Tell may hold a private pile of library knowledge.** Not encrypted — just *theirs*. They have it
here, and registering the Tell with an Atlas must not hand it over. So discovery cannot be a
side-effect of registration; **it has to be an act.**

Which is the same shape as the public-project-restricted-contribution case: a public item that not
everyone may write to, because writing is governed by the hooks and not by the library. Read and
write are already separate here; **public and discoverable have to be separated the same way.**

### The new relationship: a library registers to a Tell

A council registering its findings into a library is not the same act as sending an anecdote, so a
registration flow is in the cards — and the words that go with it are **a library registers to a
Tell**. That phrase has not existed before, and it has been a long time since anything new registered
to anything, so it deserves to be designed rather than assumed by analogy.

Open inside it: what a library's registration *grants* (enumeration? ingest? both, separately?), and
whether de-registration leaves the Atlas holding a stale index.

## 4. The Tell is the authentication control point — probably

Separate from discovery, and possibly the more load-bearing of the two.

**Discoverability and reachability are not the same thing.** A Tell server is not public or
discoverable, and that says nothing about whether the people inside it can talk to it. They can. What
is missing is where they *authenticate*.

The instinct, and it is a good one: **if a Tell is exposed at all, the Tell is the control point, for
the whole Tell.** One passkey, usable across the services running on it. The alternative — the
library authenticating separately from every other tool on the same node — means a member who signed
up for a Tell does not feel signed up for the things on it, which is close to the opposite of the
point.

To be explicit about what this is *not*: **no device accounts are auto-created for anybody.** Nobody
is enrolled by being nearby. The claim is only that when a person does make a passkey, one is enough.

**The collision to resolve before building it.** A passkey is scoped to an RP ID, and D12 already
ruled *one RP ID, at the `you` keeper*. "The Tell is the control point" and "one RP ID at `you`" are
either the same statement seen from two ends — the Tell is where you *use* it, `you` is where it
lives — or they are in conflict. **Nobody has checked which.** That check is the next real piece of
work here, and it belongs in `anecdote.channel/docs/decisions.md`, not in this repo.

Related and unsolved: exposing a public data pile at all (journal exhibits, for instance) needs both
passkey authentication and a name on the DNS system. The Tell is the only thing in the picture that
plausibly has both.

## 3. Where does the `you` engine belong — the library, or the node running it?

*(§4 below is the same question from the other direction, and leans the same way.)*

Stated both ways in the same breath, and **the node is the better instinct.** A library does not
authenticate anybody (see the no-library-card section in the README); the thing a person authorizes
*against* is the node they are standing on. Mounting `.you-engine` here would imply an identity
relationship the design explicitly does not want.

The counter-case: if a library ever wants a voucher on a stable identity — not to gate reading, but
because it wants to know that the same masked person came back — the passkey a person already carries
is what it would want, and it has to reach it somehow.

**Leaning: the node mounts `.you-engine`; the library never does.** Not settled.

### Sharpened: it is not required, *unless* it is how a grant is understood

Walking it through settles most of it. A person does not need the `you` engine to **get into** a
Tell. They might need it to **look at things on the Tell that are managed outside it** — and library
content is exactly that, because **library content never gets written into the Tell.** It is not
clear what that would even mean.

The one thing it plausibly means is **notification**: the Tell tells you when something entered the
library. That is a natural fit — delivery is already a Tell's job — and it may turn out to be part of
what registering a library to a Tell *grants* (see §2). It requires no identity engine.

So: **the `you` engine is not required — unless it is the way a grant to take something out of the
library is understood.** That is the whole hinge, and it is now the only version of this question
worth asking.

## 5. The library keeps its bottles in data-piles, and that is a custody proof

Not an identity question, but it is what §3's hinge turns on.

**Assume everything the library holds travels as a bottle**, because that is how everything travels
now. It does not strictly have to: a library may keep files that need no bottle and **package one in
a clean bottle to send it** — D17's canonical empty bottle, doing exactly the job it was named for.
The bottle stays the target either way.

Now put those bottles in **data-piles**, and three things fall out:

1. **When a thing entered the ecosystem** is legible from the git log, without anyone maintaining a
   separate accession record.
2. **You cannot write to the bottle without getting it out of the pile** — which is the outer of the
   two hook layers (`civic-node` `OPEN-QUESTIONS.md` §AA), arriving here as a practical consequence
   rather than as a rule someone imposed.
3. **The pile is a stewardship proof.** This is the new part and the sharp one.

### Custody, not existence

A signed bottle proves **the thing exists and this is its version**. A library holding that bottle in
a pile proves something strictly more: **that this library has it, and has had it since then.** Those
are different claims and only the second one is what a library is *for*.

The mechanism is ordinary — run the thing through the machine that puts it in a pile, and it is
logged there permanently and can be revealed repeatedly. What it buys is not novel cryptography; it
is that custody becomes a fact somebody can check.

### And explicitly not a redaction service

**A library should not be doing redaction footwork.** Its job is not to reveal-with-redaction; you
may already have the full documents, and it is not the library's business to be the one deciding what
of them you see. Piles support redaction because piles support it for their own owners — that
capability is theirs, not a service the library offers on others' behalf. If library work starts
requiring redaction judgement, that is a signal something has been put in the wrong place.

## 6. The caching role — one role, or two?

`status: draft` — adopted 2026-09-08, and the open part is the split.

[`BOTTLES.md`](BOTTLES.md) §3 records the library serving web-cache bottles as a front end when the
web is down. The petition it came from flagged its own likeliest error and it is worth keeping
sharp:

**Serving your own captures back to you, and serving the community's captures to strangers, have
very different trust properties.** The item treats them as one flow because that is how the operator
described it. They may be two roles that share machinery.

The distinction that would settle it: whether the library is ever asserting anything about a capture
it did not take. If it is, that is a claim about somebody else's bytes and it wants its own posture —
which is close to admission, which is [§7](#7-does-the-library-need-a-third-seat).

## 7. Does the library need a third seat?

`status: draft` — raised by the ingest, not by a seat. **Seating is the operator's act.**

Two seats exist. `clerk` synthesises what is in the stacks; `no-card` defends borrowing working with
this software switched off. Neither holds what the two adopted petitions actually ask about:

- *Are our holdings ready to be bottled?*
- *Are our archives being topped up?*
- *Should this have been admitted at all?*

`clerk`'s own `out-of-scope` already says it: *"Admission. Whether a thing belongs in the library is
a different question and probably a different seat."* The ingest is the first time that gap has had
concrete work sitting in it rather than being a prediction.

**Not proposing one, and deliberately not drafting a constituency.** A seat whose constituency was
guessed is worse than an empty chair. Recorded so the next person to open `advocate.yml` sees that
the question has stopped being hypothetical.

> **A third seat arrived 2026-09-11, and it is not this one.** `stacks` studies where the bytes
> may sit, seated from a petition that asked for it by name and supplied its own constituency in
> the operator's words. **The admission gap above is untouched** — *should this have been admitted
> at all* still has no seat, and the arithmetic of "two seats exist" no longer being true must not
> be read as this question having been answered. It has only stopped being the only thing missing.

## 8. Would a constituency-bounded library still be a library?

`status: draft` — raised 2026-09-08 by the onboarding split, and larger than the split.

The prospect that a library is **bounded by geoJSON** is what makes bottle-borne onboarding
necessary rather than merely convenient. It is recorded here because it is a claim about **who this
library is for**, and nothing in this repository has said one before.

It sits awkwardly against two things already written down:

- **No library card.** The README's load-bearing property is that walking up and reading the thing
  requires nothing from this software. A constituency is not a card — it does not gate *reading* —
  but they are close enough that the distinction has to be made deliberately rather than assumed.
- **Real libraries, and redundancy.** Two buildings across a city both listing a book is redundancy,
  not conflict. A geographic bound is a different axis from that and may interact with it.

The question is not whether a library *may* be bounded. It is **what the bound governs**: whom it
enumerates for, whom it admits, whom it serves bytes to — plausibly three different answers. Reading
is the one that must not be bounded, if *no library card* means anything.

**Not resolving it.** Onboarding is being worked out with `bottles.anecdote.channel` directly; this
entry exists so the larger question is not settled silently as a side effect of that.

## 9. Are peerage and residency two axes, or one file?

`status: draft` — raised 2026-09-13 by [`PEERS.md`](PEERS.md), which cannot answer it from inside
this repository.

The `peers:` block was put in `residency.yml` for one good reason and one weak one. The good
reason: **a node reading a mounted engine should learn the whole arrangement in one read**, which
is the same argument that put `provides:` there rather than in a second file. The weak one: it is
where the other blocks already were.

But the two axes are not obviously the same axis. **Residency is a relationship with a host** —
what an engine asks of the node it is mounted in, and what a library offers a resident. **Peerage
is a relationship with a sibling** — what this engine leans on, which has nothing to do with who
mounted it and is true of the engine standing alone in a terminal. A `.stagecraft-engine` cloned
by itself has peers and has no residency.

Three ways it could be wrong, in increasing order of expense:

- **Harmless.** One file, two blocks, and nobody is confused. The current bet.
- **A word collision.** `residency.yml` says *"read from two ends"* about `wants:`/`serves:`
  versus `provides:`. `peers:` is a third end, and a file with three ends is a file that will
  eventually be read wrong by somebody who learned two of them.
- **A wrong home.** If peerage belongs to the engine and residency belongs to the mount, then an
  engine that is never mounted anywhere still owes a peer declaration and currently has no file to
  put it in. That is the case that would force a split.

**Not resolving it here.** The convention has exactly one implementation — this repository — and a
convention with one implementation has not yet been tested by anything. The evidence that decides
it is the second engine to ship a `peers:` block, and the question that matters then is whether
its author reached for `residency.yml` unprompted.

## 10. A project holds more than one category's worth of obligation, and cannot say so

`status: draft` — raised 2026-09-13 by the [artist-lockers fitting](adoption/worked/artist-lockers.md).

[`CATEGORIES.md`](CATEGORIES.md) reserves words that name **what a level of a hostname means**, and
[`SEATS.md`](SEATS.md) attaches a health rule to each. Both assume one word answers for one thing.
The first real project fitted against them needed three at once:

- the **repository** is `trade` — a template other parties copy, whose health rule is *the template
  still builds, and nobody is wedged into a workaround*;
- its **holdings** are `media` — whose health rule is *the artifact still plays*;
- and the **authors** inside it are owed something shaped like `voices` — *attribution is intact and
  the writer can still withdraw* — which no part of the project currently provides, because nobody
  had posed the question.

Those are three different clocks. A build breaks and is noticed the same afternoon; a codec dies in
ten years; a consent question surfaces the day somebody asks to be removed. **A single category
assignment cannot carry three health rules**, and today there is nowhere to write down that a
project answers to more than one.

What is *not* the answer, at least not obviously: multiple categories. The words are canonical
because a thing is forced to be one category — that is the whole federation argument in
`CATEGORIES.md`, and letting a project claim three would dissolve it. The likelier shape is that a
holding is categorised separately from the repository that serves it, and that obligations toward
*people in* a holding are a third thing again that is not a category at all.

**Not resolving it.** It touches what promotes a tag to a category, which
[`CATEGORIES.md`](CATEGORIES.md) already hands to `anecdote.channel`. Recorded here because the
fitting found it and the reasoning should not have to be re-derived by the next one.

## 11. What does a library exhibit when it cannot serve a README?

`status: draft` — raised 2026-09-13 by [`EXHIBIT.md`](EXHIBIT.md), which decides that README is the
index and then runs out of ground.

The scheme assumes a library can serve a markdown file at its bare address. **A library is a
branch**, and `store:` in [`residency.yml`](residency.yml) already anticipates that a second one
might not be a filesystem at all. An IPFS-backed library plausibly has an index and nothing that
answers a request for `README.md` — the content is *in the bottle*, and opening the bottle is what
produces something to read.

Which suggests, without settling it, that the exhibit is not a file but **a thing a bottle
contains**, and that serving a README is one implementation of exhibiting rather than the
definition of it. If that is right, `EXHIBIT.md` currently describes the filesystem case and calls
it the general one.

Three ways this could land, and they are not equally cheap:

- **The README is a build artifact of the branch**, compiled into whatever fragment the library
  contributes, and each store implements *producing* one. Cheapest, and it keeps the strong posture.
- **The exhibit lives in a bottle** and a store that cannot serve files serves the bottle instead.
  Consistent with bottles being the transit object, and it means a stranger's first contact is the
  same artifact whether they arrived by URL or by QR.
- **Some libraries do not exhibit.** Legitimate, and it costs the guarantee that made the strong
  posture worth taking — *there is always a door* stops being true.

**Not resolving it.** It needs the branch-fragment build to exist first, and that does not.

## Related, elsewhere

- **The control QR.** The `discoverywritten` work wants it for onboarding onto the bottle surface.
  The thought worth carrying: **it is more powerful if what you receive is a *library item* — which
  is a bottle — than a bare bottle.** An item arrives with provenance, a place it came from and
  something that enumerates it; a bare bottle arrives with none of that.
- **The signers-list amendment request** — the one message a borrower may need to send. No shape yet;
  must stay optional and stay small.
- `civic-node` `OPEN-QUESTIONS.md` §AA — the two layers of hooks, and loaning as a grant of write.
