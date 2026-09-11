# library.anecdote.channel

**An engine, and the domain fact that goes with it.** A library keeps knowledge somebody gave it,
enumerates what it has, and lends it out — and the lending needs nothing from the library at all.

> Stubbed 2026-09-03. Design lives in
> [`civic-node/docs/proto-issues/library-the-knowledge-kind.md`](https://github.com/FCCN-ANTIBODY/civic-node/blob/main/docs/proto-issues/library-the-knowledge-kind.md).
> Everything here is `draft` in the [`STATUS.md`](.advocate-engine/STATUS.md) sense.

## The category, and why the engine is not named after it

The constellation had a category for people writing (**voices**), for broadcast (**media**), for
business (**trade**), for the civic node (**city**), and — once bottles arrived — for files. It had
none for **knowledge**. That one is **library**: singular on purpose, because it should read as *the
place*, one big library with a lot in it.

**A category is not an engine.** A trade site does not need a trade engine. A category names what a
level of a hostname *means*; an engine is machinery a node *mounts*. The two axes are independent and
usually do not share a word — `bottles` is the one place they already coincided and `library` is the
second, and that is vocabulary, not a rule. **Do not go looking for the engine that matches a
category name.** This repo exists because *this* category needs machinery — enumeration, admission,
a clerk — not because categories get engines.

*(Tried and rejected on the way to the word: **knowledge**, **experience**. `library` won on being
the plainest word a stranger already understands.)*

## What a library is for

**Its own enumeration mission.** An Atlas has to go and build an index; a library is already listing
what is inside it, because that is what a library is. **A library plugged into an Atlas is that whole
index on tap.** That asymmetry is the reason this is a kind and not a folder.

It is not compulsory reporting (antidote's job with poll data), and not the transparency
documentation a node publishes about its own traffic and registrations. It is nearer to a person who
wrote something down and **elects to have the public witness it if they need it.**

## No library card

The load-bearing property, and the easiest one to lose by accident. Checking a data-bottle out,
writing to it, and putting it back **requires nothing from this software.** The bottle carries its
own manifest and its own rule for how a diff may be applied to a frozen capsule, so the editability —
and more importantly the after-the-fact validation that a change came from who it claims — falls out
of the bottle spec working by itself.

- **No front desk.** Nothing central decides whether a change is allowed. It is allowed implicitly by
  what the artifact says, or it is not. A library that adjudicates has to be online, trusted and
  correct, and this design refused all three.
- **An owner updating their own bottle uses the identical mechanism as a borrower returning an edited
  one.** If those ever need different code paths, something went wrong upstream.
- **Stocking is self-service too.** No management layer for the people putting things in, either.
- **The only real reason to talk to a library** is to ask for a specific checkout — *put my name on
  the signers, with an expiration.* A request to amend a list, not an authentication. Optional: a
  bottle may arrive with its signers already set.
- **A library card is an establishment's local concern**, for their own metrics. Legitimate, and
  theirs. It must never become a prerequisite, because *walk up and read the thing without
  infrastructure* is the kind of library this is for.

## Holding, and the bytes it does not have

**A library that only points at things is a catalogue.** The distinguishing claim — the one custody
is for — is *this library has it, and has had it since then*, and that requires holding the bytes.

The bytes live in **bottles**, in **data-piles**. That is not an implementation preference; it is
what makes the custody claim checkable, and it is worked out in [`OPEN.md` §5](OPEN.md).

Two things follow that are easy to get backwards:

- **The library does not own the bottle.** It holds one. The format, the renderings and the player
  belong elsewhere — see [`BOTTLES.md`](BOTTLES.md), which is deliberately a list of requirements
  and not a design.
- **Holding is not adjudicating.** A bottle arriving as a *construction* rather than a clean seal
  should be visible as one, and that is the end of the library's involvement. *We want a way to
  trust bytes; we do not want to be the ones deciding how to trust them.*

Once it can hold bytes, a thing it can do that a mirror cannot: serve **web-cache bottles as a front
end when the web is down**, topped up by intermittent connectivity and fast-forwarded to whoever
already has an older copy. That role is adopted in [`BOTTLES.md`](BOTTLES.md) §3 and its open edge —
whether serving your own captures and serving strangers' are one role or two — is
[`OPEN.md` §6](OPEN.md).

## Onboarding is ours, generally — and it is not ours exclusively

**The library onboards people.** That is the general case and it belongs here.

**The exception is the one that matters**, and it is not a gap in this repository: somebody who
encounters a bottle in the wild, carrying a control code, **onboards with the bottle.** They do not
have to already be on anything, and they should not have to find us first.

The reason is a property of this library rather than a shortcoming of it:

> **A library may be constituency-bounded** — by geoJSON, later. A constituency-bounded onboarder
> cannot be the only door, because the person who most needs a door is a stranger holding an
> artifact, and a stranger is in no constituency by definition.

So the split is not a division of labour that could have gone the other way. **The bottle is the free
transit object** — it moves, and nothing else in the picture does — which makes it the thing a
stranger actually encounters. It gets the job by being portable, not by being suited to it.

What this library has to keep straight, and the thing most likely to be got wrong here:

- **A control code is not ours to issue or revoke.** A bottle exercises authority at minting time and
  never at runtime. If this repository ever wants to revoke one, it has wanted something that does
  not exist.
- **We may be the party that honours one.** A code is an assertion that the holder may be admitted,
  to whoever is later in a position to admit them. A library stacked on a node is a plausible
  *whoever*. Whether it is *the* one is open.
- **Admitting a stranger is not the same as serving a constituency.** If those ever need to be the
  same mechanism, something has gone wrong — which is the same shape as the no-library-card rule and
  should be defended by the same instinct.

The seam is still open and it is being worked out in `bottles.anecdote.channel`'s
[`ONBOARDING.md`](https://github.com/FCCN-ANTIBODY/bottles.anecdote.channel/blob/main/ONBOARDING.md),
alongside [`OPEN.md` §8](OPEN.md) here.

## Real libraries, and redundancy

There are literal libraries and they will register under this category. Two buildings across a city
both listing a book is **redundancy, not conflict** — the useful fact that the thing is available in
more than one place. **Being forced to be one category is what makes it canonical; being forced to be
one collection would not.**

Lending, holding, returning and late fees are closer to **trade** than to knowledge, which is why a
physical library reads as two categories at once. The library holds and enumerates; the loan
mechanics belong to the bottle.

## The clerk

One seat, named because its shape is unusual. A **clerk** synthesises notes from what it sees —
*"between these dates, Chrome updated from this to that"* — and keeps them in a stacks area with
whatever filing system it can stand. Expected to be a bit chaotic and still skimmable by an agent
passing through.

**The clerk's job is not to write documentation that gets cited instead of the real thing.** It
synthesises from what it observes and re-reads its own notes before speaking about a resource. The
bar is to *observe proficiently*, and to be sharpened when better information turns up.

## What it mounts

| mounted | as | for | settled? |
| --- | --- | --- | --- |
| `advocate.anecdote.channel` | `.advocate-engine` | it has seats; the clerk is one | **yes** |
| `journal.anecdote.channel` | `.journal-engine` | it has to publish directories | likely |
| `bottles.anecdote.channel` | `.bottles-engine` | it is how the library holds bytes at all | **exists since 2026-09-08; not mounted yet** |
| `you.anecdote.channel` | `.you-engine` | a person authorizing against it | **open — see [`OPEN.md`](OPEN.md)** |

`.bottles-engine` is **not mounted** and nothing here depends on it yet.
[`BOTTLES.md`](BOTTLES.md) is what this library needs from it, and the repository now exists to
answer that: [`FCCN-ANTIBODY/bottles.anecdote.channel`](https://github.com/FCCN-ANTIBODY/bottles.anecdote.channel).

**And "consumer" does not mean downstream.** The library consumes bottles by being **stacked with
them on a node repository** — a civic node, a station node, or a pure communications node. They meet
on a node; neither repository is upstream of the other. That distinction is what puts the onboarding
boundary in the right place, below.
[`BOTTLES.md`](BOTTLES.md) is what this library would need from it, written as a consumer so that
provisioning the repository has something to build against.

## What it is mounted *into*, and what it provides

The mount table above is what this engine takes. The other direction is a relationship the
library had no word for until 2026-09-11: **residency.** An engine mounted beside this one on a
node does not contribute and is not merely held — **it lives here and keeps working**, and it
gets a wing.

`.library-engine` is a resident too, of whatever node mounts it, and it is not privileged for
being a library. What it asks for and what it offers are in one file,
[`residency.yml`](residency.yml), read from two ends. The reasoning is
[`RESIDENCY.md`](RESIDENCY.md).

Three things worth knowing without opening either:

- **The mount name is the claim.** Anything mounted as `.<name>-engine` may hold a wing named
  `<name>`, and this library's caretaking does not apply inside it.
- **The prefix `library` is canonical** — so an outside tool can guess and be right. The key
  exists mostly so a library can say it is **not on a path at all**, which is what an IPFS store
  would need.
- **The node owns the CPU.** Which seats exist and what they attend is the library's to say;
  whether anything runs at all is the node's, and the residency claim is a menu rather than a
  startup script.

## Open

Live questions, one of them large. See [`OPEN.md`](OPEN.md). §1 (does `library` subsume `bottles`)
has been answered from outside — it does not — but the constellation decision record is still owed.
