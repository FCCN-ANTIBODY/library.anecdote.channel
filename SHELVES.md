# `share/` and `build/` — the shelves a library keeps for itself

`status: draft` — written 2026-09-13, from the operator's decision to stop letting moniker groups
squat at a library's top level:

> *"Looking at the file system, and like other distributed apps, I'm pretty sure I should be using
> the file path prefix `share`. In particular, it stands next to `build`. `build` is, like, for
> intermediates within the library. If there is tooling that is actively drawing on what's in
> there, `share` becomes a little bit more public version of that."*

**Nothing has moved.** This is the vocabulary, written down so that the move is a `git mv` and not
an argument.

## The problem: three kinds of name, and one of them is squatting

A library's top level holds names that mean genuinely different things, and until now only two of
them were declared:

| kind | looks like | declared in | who names it |
| --- | --- | --- | --- |
| **a category** | a bare reserved word — `trade`, `voices`, `city` | [`CATEGORIES.md`](CATEGORIES.md) | this repository, in advance |
| **a wing** | `.<name>-engine` | [`RESIDENCY.md`](RESIDENCY.md) | the mount that claimed it |
| **a shelf** | `share/`, `build/` | **this document** | the library, for its own working |

And a fourth that is not a kind at all — **a moniker group.** `FCCN-ANTIBODY/`, `Chaevity/`,
`NoodlesDevelopment/`, `FCPM/`, `Mythulu/`, `NCCV/`, `DiscoveryWritten/`: org names sitting at the
top level beside canon words, which [`RESIDENCY.md`](RESIDENCY.md) already admits is *"a mix of canon
words, organisational monikers and project clusters, and that inconsistency is already tolerated on
purpose."*

Tolerated, and now nameable. **Most moniker groups are there for exactly one reason: the library is
sharing those references.** That is not a category and it is not a wing. It is a shelf, and the
shelf is `share/`.

## `share/` — what the library puts forward

**The prefix for things held in order to be handed on.** A reference the library keeps so that
somebody else can get at it: engines it shares, pointers it publishes, the groups that exist only
because they are being offered.

The precedent is the filesystem's and it is the reason the word needs no explanation: `share` is
already, everywhere, *the stuff that is here for other people*. It stands next to `build` the way
`/usr/share` stands next to `/usr/lib`, and a distributed app reading a library it did not build
can guess `share/` and be right.

Two properties worth stating because they are easy to lose:

- **`share/` is not a synonym for public.** It says *this is held to be handed on*, which is a
  statement about intent. Whether it is served to anyone is the selection below, and they are
  deliberately different questions — the same separation `disposition:` already makes at the label
  level in [`residency.yml`](residency.yml).
- **`share/` is where the moniker groups go, not a replacement for them.** `share/FCCN-ANTIBODY/`
  keeps the group; it stops the group from claiming a top-level word.

## `build/` — intermediates, and the reason it is not a cache

**The prefix for things the library made, that it could make again — except when it could not.**

`build/` already exists in a library as an empty advertisement, which was correct and is now
explained. It is `lib`-shaped: working material that tooling actively draws on, deterministic,
regenerable in principle.

The load-bearing case, in the operator's terms, is the one that makes `build/` more than a cache:

> The journal engine knows how to pull fragments from its citation journals and use those. Today
> that works at the *superficial* level — a submodule head reference, so the artifact can be
> fetched when it is wanted. **If we lose connectivity, we cannot fetch it.** So the artifact goes
> to `build/`, at a canonical path, and that is where it is sourced from deterministically.

Two things that buys, and the second is the one that names the failure:

1. **It survives losing the network.** A pin is a promise that something is retrievable. `build/`
   holds the retrieved thing.
2. **It stops the babies getting mixed up at the hospital.** A fragment pulled from a citation
   journal has to land at a path that says *which* journal, at *which* pin, for *which* build. A
   flat cache keyed on convenience is how two builds end up sharing one artifact and nobody can
   tell which produced it.

So `build/` is **deterministic by path**, not merely present. The path is part of the artifact.

## Why the explosion is acceptable

Adding shelves alongside seven category words and an unbounded set of wings means a library's top
level fans out, and that is a real cost the operator named directly:

> *"It's important for organization. But what it means is that, like, we're exploding a bunch of
> separate things. The comfort we can take is that we're having to do it because we happen to own
> this project, and we have several concerns to manage, so it makes sense."*

The comfort is exact and it is worth holding onto: **the fan-out is a property of running several
concerns, not of the scheme.** A library with one concern has one folder. The station's library is
wide because the station does a lot, and a design that hid that would be hiding the truth about the
station.

What the scheme buys in exchange is that **the library operator knows, by looking, what is shared,
what is intermediate, and what is put forward under a category.** That is the whole trade.

### The same project, on two shelves, is normal

`share/DiscoveryWritten/stagecraft` and a trade-oriented site for stagecraft under `trade/` are
**not a duplication to resolve.** One is a shared reference; the other is a presentation aimed at a
different audience. Same subject, different documents, different readers.

This is the same shape as *"`library` inside a library is legitimate and not a mistake"* in
[`CATEGORIES.md`](CATEGORIES.md): being forced to be one *category* is what makes a word canonical;
being forced to appear in one *place* was never the claim.

## The selection: `public:` and `except:`

A library is a branch, and a build has to know what that branch is willing to put into a fragment.
The requirement is stated as a refusal:

> **Nobody should be fighting an include/exclude system.** Listing everything is intolerable for a
> large library, and a two-list scheme with precedence rules is the thing that makes people give up
> and publish either too much or nothing.

So: **one boolean, and the exceptions to it.**

```yaml
# a public library that keeps its intermediates to itself
public: true
except:
  - build/
```

```yaml
# a private library that puts one wing forward anyway
public: false
except:
  - trade/
```

`except:` always means *the other way from `public:`*. There is no second list, no ordering, and no
way to write a rule that contradicts another rule. The cost is that you cannot express an exception
to an exception, which is the intended cost.

Worked, for the two libraries that exist:

| library | setting | meaning |
| --- | --- | --- |
| the civic node's | `public: true` | it is a public body; the library is the public record |
| the station's | `public: false`, `except: [trade/]` | a personal node, with trade material it does put forward |

### The addresses in `except:` belong to the store, not to this file

`trade/` and `build/` are **file paths**, because `store: filesystem` is the only value anything
implements today and a path with a trailing slash is that store's idiom for *and everything under
it*.

A library with `store: ipfs` addresses its holdings differently, and `except:` will have to accept
whatever that store's addressing is. **This is not a general targeting language and should not
become one.** The rule: `except:` entries are opaque to the library engine and interpreted by the
store. A store that cannot interpret an entry must refuse the build loudly rather than publish on
a guess — publishing on a guess is the one failure this whole scheme exists to prevent.

### Where it lives

Proposed: **`library.yml` at the root of the library branch.** Not in `residency.yml`, and the
distinction matters — `provides:` in that file says what *the engine* offers a host, and is the same
in every library. Publicity is a fact about **one instance**, decided by whoever runs that branch,
and a per-instance fact in a per-engine file is the second surface problem again
([`PEERS.md`](PEERS.md)).

Alternative not taken: a key in the host's own configuration. Rejected because the branch is the
library, and a library that cannot say for itself whether it is public has to be asked — which is a
front desk.

## Branch fragments, and what is not built

**None of the following exists.** It is recorded because the shelves only make sense inside it.

A library is a branch; `main` is where the site is built. So when `main` builds, it has to **compile
the fragment each library branch contributes** — which means the library, in this act, is a
compiler over its own branches, and each branch can have its own implementation.

Three open edges, in the order they will bite:

- **A fragment's UI is not uniform.** A filesystem-backed branch can produce a rich exhibit. An
  IPFS-backed one may manage an index and nothing else, with the content reachable only by opening
  a bottle. So *"what a fragment looks like"* is per-store, and the build cannot assume. This is
  [`OPEN.md` §11](OPEN.md) arriving from the other direction.
- **The build artifact may live on the branch.** A fragment cached into `build/` on the library
  branch is not odd — the branch is where that library's working material belongs, and keeping it
  there means `main` never carries another library's intermediates.
- **Nothing has moved yet, and the audit says why.** `station-node/docs/the-library-as-a-branch.md`
  found that moving the held groups off `main` would silently cost the advocate council twelve of
  thirteen registry entries, because a name is known by `.gitmodules` on `main`. **That is the
  blocker, it is in somebody else's repository, and this document does not clear it.**

## What this document does not do

- **It does not move anything.** Not one `git mv`. The vocabulary first, so the move is mechanical.
- **It does not make `share/` or `build/` categories.** They are shelves. A shelf is a library's own
  working prefix; a category is a claim about what a word means constellation-wide. They are
  reserved against collision in [`CATEGORIES.md`](CATEGORIES.md) — *spoken for, and not categories*
  — which is the whole reason this could be written without asking anyone.
- **It does not decide what a fragment is.** Only that shelves exist inside whatever it turns out
  to be.
