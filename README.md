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
| `you.anecdote.channel` | `.you-engine` | a person authorizing against it | **open — see [`OPEN.md`](OPEN.md)** |

## Open

Three live questions, one of them large. See [`OPEN.md`](OPEN.md).
