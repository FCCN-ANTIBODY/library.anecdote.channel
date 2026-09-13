# `trade` — the door for a working project

`status: draft` — written 2026-09-13, from the [artist-lockers fitting](worked/artist-lockers.md).

**You are here because you have a thing that works.** A tool, a shop, a service, a template other
people copy, a site that does a job. `trade` is *business, money or not* — the word covers the
unpaid tool and the paid one identically, because the failure modes are the same and the money is
not what makes them.

This door does not restate [`../CATEGORIES.md`](../CATEGORIES.md) or
[`../ADOPTING.md`](../ADOPTING.md). Read `ADOPTING.md` first if you do not yet know what an engine
or a bottle is; nothing below re-explains them.

## The distinction that trips up every trade adopter, in the first five minutes

**The category of your repository and the category of what it serves are different questions, and
you will be asked both.**

A tool that publishes music is `trade` as a repository and `media` as a holding. A template that
other writers copy to publish essays is `trade`, and every copy of it is `voices`. This is not
pedantry and it is not a taxonomy problem — it decides *which health rules apply to which part of
your project*, and they are genuinely different rules. Your build breaking is a trade failure.
Your artifacts becoming undecodable is a media failure. One of those you notice the same day.

So: **claim `trade` for the repository, and say separately what its holdings are.** Nobody has to
adjudicate that for you, and getting it wrong costs a line in a file.

## What healthy means here, and the way it fails

The row from [`../CATEGORIES.md`](../CATEGORIES.md), which is short because the expansion belongs
here:

> `trade` — a nameplate still resolves to a live party; a template still builds; nobody is wedged
> into a workaround by a gap in *our* tools.
> **Fails as:** everything is present and nothing works; the gap is invisible from inside any one
> holding.

Three failures, and the third is the one this door exists for.

**1. The nameplate stops resolving.** The party is gone, the domain lapsed, the contact address
bounces, and the listing still looks perfect. Trade is the category where the *pointer* rots faster
than the content, because a business is a live party and a poem is not.

**2. The template stops building.** A trade repo is very often a thing other people copy —
artist-lockers says so in its first line. A template that no longer builds has failed for everyone
who has not yet copied it, and for nobody who already did, which is exactly why it goes unnoticed.

**3. Somebody is wedged into a workaround, and we cannot see it.** This is the interesting one.

### The wedge, and why it is our failure and not yours

A working project with a real problem does not wait for us. It solves the problem, ships, and moves
on. The solution goes in *their* repository, where it is invisible to us, and it looks from every
angle like a normal engineering decision — because it *is* one.

From inside that project nothing is wrong. From inside any single holding nothing is wrong. The gap
only exists in the aggregate: **ten trade adopters independently building the same missing piece,
none of them able to see the other nine.** No amount of care by any one of them surfaces it.

So the ask this door makes of you is the one thing that cannot be automated:

> **When you work around a gap in our tools, tell us.** Not a bug report and not a feature request
> — a sentence saying what you had to build yourself. That is the entire mechanism, and it is a
> [petition](https://github.com/FCCN-ANTIBODY/library.anecdote.channel), filed against whichever
> repository should have had it.

We would rather hear *"I had to write my own pinning layer"* six months late than not at all. The
artist-lockers fitting exists because exactly that happened and nobody had told anyone.

## What to take, ranked by your pain

Not by our architecture. In the order these actually hurt a trade project:

| if this is true of you | take | it is worth it because |
| --- | --- | --- |
| **something you serve lives on a clock you do not control** — signed CDN links, an expiring host, a third-party gateway | **bottles** | the artifact stops depending on the link that carried it. This is the one that pays for itself first |
| **you already have an index, a catalogue, or a listing page** | **library** | you have most of one already; you gain enumeration others can plug into, and a custody claim you cannot currently make |
| **somebody needs to reach you who holds nothing of yours** — no account with you, no seat in your Discord, no repository access | **tell** | it is the only answer we have to that question, and it is inert until spoken to |
| **there is a maintenance concern nobody has time for** | **advocate** | cheapest thing on the list. No listener, no runtime, opens pull requests on its own branch, runs by hand from a terminal |
| **you want to be found** | **atlas** | routability. Deliberately last: discoverable and joinable are separate decisions and you should make them separately |

**Everything above is independently adoptable.** Taking one does not oblige you to the next. If
you take exactly one thing from this page and it is bottles, that is a complete and correct
adoption.

## What you must decide now, and what you may decide later

An adopter is entitled to know which doors close behind them. **Almost none of ours do**, and the
exceptions are worth stating exactly.

### Decide now — because it is cheap now and a migration later

- **Your word.** `trade`, and separately what your holdings are. It is a line in a file today. A
  reserved word taken back is a migration paid by whoever federated with you in between —
  [`../CATEGORIES.md`](../CATEGORIES.md) is blunt about this and it is the only irreversible thing
  on this page.

### Decide now — because doing it later costs a rewrite of your own code

- **Whether artifacts are addressed by content or by location.** If you are about to build a
  caching, pinning or mirroring layer, that is the bottle-shaped decision, and retrofitting it
  means rewriting every reference you have already stored. Nothing forces you toward bottles; the
  cost of *changing your mind later* is what makes this a now-question.

### Decide later — genuinely, and we will not ask again

- **Which engines to mount.** A mount is a `git submodule add` and an unmount is a `git rm`.
- **Whether to be discoverable.** Listing on an Atlas is reversible and separate from admitting
  anyone.
- **Whether to run anything.** A mounted engine starts nothing. **The claim is a menu, not a
  startup script** — you order from it by installing a job, and not ordering is a permanent,
  supported, unremarkable state.
- **Whether to seat an advocate**, and how many. Seats are per-concern and each lives on its own
  branch.
- **Whether to accept anything you are offered.** Being held by a library, listed on an atlas, or
  petitioned by a seat obliges you to nothing.

### Not yours to decide, and not ours either

- **A control code is not issued or revoked by anybody at runtime.** A bottle exercises authority
  at minting time. If you find yourself wanting to revoke one, you want something that does not
  exist — say so rather than building around it.

## What we do not have yet

Named plainly, because a gap named is a petition and a gap unnamed is another wedge:

- **`bottles` is `draft`.** The vocabulary is settled and the wire format is not. A trade adopter
  who needs bottles *today* will be implementing against a moving target, and should say so loudly
  rather than quietly forking.
- **There is no trade-specific seat.** [`../SEATS.md`](../SEATS.md) describes category seats; the
  `trade` one is not written, which means nothing is currently watching for dead nameplates or
  templates that stopped building.
- **No mechanism finds the wedge automatically.** The aggregate view that would reveal ten
  adopters solving one problem does not exist. Today the mechanism is that you tell us, and that
  is a weakness in our design, not a duty of yours.
- **`library` is `draft` too**, and it is the repository this door lives in. Adopting it means
  adopting a stub with a clear head about what it is for.
