# What this library needs from a bottle engine

`status: draft` — adopted 2026-09-08 from two petitions filed against this repository.

**The library holds knowledge. Bottles are how it holds it.** This document is the *consumer's*
half of that relationship: what a library needs in order to hold bytes at all, written down before
`bottles.anecdote.channel` exists so that provisioning it has something to build against.

> **This repository does not own the bottle format.** Everything in §1 is a requirement, not a
> design. If it reads like a spec, that is the failure mode to watch for — see
> [What this repository will not own](#what-this-repository-will-not-own).

> **Answered 2026-09-08.** [`bottles.anecdote.channel`](https://github.com/FCCN-ANTIBODY/bottles.anecdote.channel)
> exists. This document did its job — it was the specification the stub was written against — and it
> stays as the record of what was asked for, not as a second copy of what was built.
>
> **Consumer means co-mounted, not downstream.** The two meet on a node — civic, station, or a pure
> communications node — and neither is upstream of the other.
>
> The vocabulary table has **moved** there and is deliberately not copied back.

## Why this document exists at all

This library currently points at **84 references and zero bytes**, on a workstation node, because
the intended place for bytes is a bottle and there is no engine to make one. That makes the library
a consumer of something that does not exist, and the account of what it needs is worth having on
the record even if nothing gets built for a while.

## 1. The four things, in the order they bite

### 1.1 A stored rendering that is actually small

A bottle at rest is read by **a program that already has the file**, never by a camera. Optimising
it for optical acquisition is optimising against a constraint the stored form does not have: no
quiet zone, one module to one pixel, playback as a decode rather than a duration.

The library's interest here is narrow and it is **not** compression for its own sake: a library
that holds many bottles pays the size of every one of them, forever, and it is the party that
notices first.

Worth measuring rather than assuming: whether file compression buys anything on top at this scale.

### 1.2 A player that needs no build step

A stored bottle has to be openable by a tool handed **one bottle and nothing else**. If playback
requires a build, the bottle stops being a thing you can hand someone — and handing it to someone
is the whole point.

**This is the requirement most likely to belong to somebody else.** See below.

### 1.3 Stuffing — wrapping loose bytes into a bottle

A library admits things that arrive as plain files. It needs to wrap them with the metadata worn on
the outside, so the wrapper carries the proof of what is inside.

The distinction the library cares about, because it is the one it would have to display:

- **A clean bottle is simply ready.** Nothing was injected; it is what it says it is.
- **A bottle assembled from a loose file plus injected bytes is a construction**, and it should be
  visible as one.

*We want a way to trust bytes. We do not want to be the ones deciding how to trust them.* A library
that quietly flattens those two states has started adjudicating, which is the thing this repository
exists to refuse.

### 1.4 Cold, sterile checkout

The librarian's ask, and the one the library would trade the other three for.

An agent opening a held project gets an **inert** artifact — see the node's `library/INERT.md` —
unpacks it into a work tree, and knows that what it unpacked is exactly what was sealed.

**The guarantee is worth more than the compression.** A library's claim is custody; custody with no
integrity check is a claim about a filing cabinet.

## 2. The carbonite property, which is why custody is provable

A bottle carrying a git repository **plus its hooks** is a different object from an archive of one.
It states, unequivocally, *this is the base you must commit against to be valid.*

Normally git hooks are worth nothing: they live in client space and anyone can drop them. Inside a
sealed artifact whose entire identity is the seal, they are part of the thing being distributed
rather than part of the machine running it. The version and the configuration **are** the artifact.

For this library that is not a curiosity — it is the mechanism that makes
[`OPEN.md` §5](OPEN.md) true. Holding a bottle in a data-pile proves *this library has it, and has
had it since then*, which is strictly more than a signature proves, and it is the only claim a
library is actually for.

## 3. What the library would do with it: the caching role

`status: draft` — the second petition, and a **role** rather than a requirement.

A library that can hold bottles can serve **archives of other people's websites to people who
cannot reach them**. Not a directory of references: a cache of the web, held by people, versioned,
and handed out.

> *"You don't need to hit the web because it's down, but here's what we know the last version was.
> And if we get intermittent connectivity, we will add to it. And if you check it out, we can
> fast-forward yours too."*

Four properties, each of which a plain mirror cannot do:

- **It starts from a captured bottle, not a crawl.** The input is somebody's actual browsing
  session, packed. The archive grows from real visits rather than from a spider's judgement about
  what matters. **Nothing here proposes fetching the web.**
- **Topping up is a fast-forward.** Intermittent connectivity amends a bottle rather than replacing
  it, and a holder with an older copy catches up instead of re-downloading. This is the existing
  pile machinery pointed at web content.
- **It hands out a shallow tip.** A consumer wants the current state; the library keeps the whole
  history and serves the tip. The history stays available to anyone who wants to argue about what a
  site used to say — which is most of the value and none of the download.
- **Contribution needs no new mechanism.** Community diffs land against a stated base, and the
  library squashes, rebases and re-canonicalises. The bottle system already has that shape.

### Reader view, and the one place this stops being neutral

Most captured sites will render badly. Improving a rendering is **an amendment against a canonical
base** — the same door community diffs come through — so a better reader view of a badly-built site
is a contribution the system already knows how to accept.

**That is also where neutral archiving becomes editorial**, and it should be deliberate rather than
discovered. A library is the right body to be deliberate about it; it is not a thing to let happen
by accident.

### Named as present, not answered

**Redistributing captured sites raises legal questions this repository is not qualified to
answer.** Recorded here so that nobody mistakes the silence for a finding.

## What this repository will not own

The boundary matters more than the requirements, because a stub that quietly grows a spec is how
two repositories end up implementing the same format differently.

| | owner | why |
|---|---|---|
| the wire format | `bottles.anecdote.channel` | it should be **a spec somebody can implement twice**, which it cannot be while it is a section of a consumer |
| `projected` / `enchanted` renderings | `bottles.anecdote.channel` | optical crossing is not library behaviour |
| the player / clean-room viewer | **unsettled** — `bottles` or `anecdote.channel` | flagged by both petitions as their weakest boundary; see [`OPEN.md`](OPEN.md) |
| whether a change to a bottle is allowed | **nobody** | no front desk. It is allowed by what the artifact says, or it is not. |

**Not all bottle making is library behaviour.** A desktop capture worker, a proofing tool and an
offline browser all mint bottles with no library involved. That is the argument this document is
built on, and it is the reason the requirements above are written as a consumer's account rather
than as a design.

## Vocabulary — moved, and deliberately not copied

**`bag` / `bottled` / `canonical` now live in
[`bottles.anecdote.channel`](https://github.com/FCCN-ANTIBODY/bottles.anecdote.channel).** Cite that.

The table is **not reproduced here**, and resisting the urge to leave a convenience copy is the
point: two homes for one fact is the failure this constellation keeps naming, and a copy kept "so a
reader is not left guessing" is exactly how the second home gets built. One link is not a hardship.

The one consequence this library must not forget, because it is the one a library is positioned to
break: **`canonical` is relational, not public.** It cannot be computed from a file, so this
repository may never assert it on somebody else's behalf.

## Where this came from

Adopted from the petition space at `station-node`, on the node's library addressing:

- `FCCN-ANTIBODY/library.anecdote.channel/the-bottle-engine-a-library-needs.md` — §1, §2
- `FCCN-ANTIBODY/library.anecdote.channel/serve-the-web-back-when-the-web-is-down.md` — §3
- `unplaced/bring-back-the-bottles-repository.md` — the vocabulary, and the boundary table

The first two are this repository's and are adopted here. **The third is not ours** — it asks for a
repository to exist, which is not a thing this repository can grant. It is cited because the
boundary above is taken from it.
