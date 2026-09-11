# Residency, and what it means to *provide* a library

`status: draft` — adopted 2026-09-11 from the petition
`residency-is-a-relationship-you-have-no-word-for.md`, filed against this repository on
2026-09-10 and answered here.

**The petition's complaint was not that the idea was wrong. It was that the idea was written
down on one side only** — `DiscoveryWritten/stagecraft` had a design note, a schema and a
committed `residency.yml`, and nothing in this repository contained the word *residency*. A
producer contract with no referee. This document is the referee.

## The answer: adopted

**A library has three relationships, not two.**

| | what it means | governed by |
|---|---|---|
| **holding** | the library points at your repository | never read the content — it is inert |
| **contributing** | you file something; it becomes the library's | the petition space, `intake/` |
| **residency** | **you live here, and keep working** | this document |

Residency is not a larger contribution. It is **ongoing**, it is **write**, and it belongs to
software rather than to an idea. That is why neither existing rule fits it. The alternative it
is designed against, in the operator's words: *"It's either the engines aggressively push their
way in and elbow in, or they register that residency."*

Three pieces, accepted as specified:

1. **The mount name is the claim.** `.stagecraft-engine` at a host root *is* the residency
   claim. The name comes from the mount path, so nobody types it twice and two residents cannot
   collide, because two submodules cannot share a path. The whole rule is one sentence:
   **anything mounted as `.<name>-engine` may hold a wing named `<name>`, and the library's own
   caretaking does not apply inside it.**

2. **Terms, not locations.** A `residency.yml` declares **labels and their properties**; the
   library binds labels to paths and answers `label → path` at runtime. The engine never names a
   directory and the library never guesses an intent. Move the wing to another volume, or
   reorganise the whole taxonomy — the resident never notices.

3. **`disposition` per label** — `private` / `on-request` / `public`. This is the piece this
   repository should care about most, because it closes the gap where **"in the library" gets
   read as "public"**, and it closes at the *label* rather than the wing: one resident
   legitimately holds private working state and public downloads at the same time.

Point 3 is a direct contribution to [`OPEN.md` §2](OPEN.md), which already argued that *public*
and *discoverable* have to be separated the way *read* and *write* already are. Stagecraft
proposed the mechanism; this is the acceptance it was owed.

### A wing is not a group, and that is why nothing had to wait

The library's top-level folders are a mix of canon words, organisational monikers and project
clusters, and that inconsistency is already tolerated on purpose. **Residency is a different
axis.** A resident is not a group and its wing is not a category, so whatever the group taxonomy
settles into, residents are unaffected. The two questions were being conflated; separating them
means neither blocks the other.

Wings are also disjoint from the reserved category words — see [`CATEGORIES.md`](CATEGORIES.md)
if it has landed. A wing is named by a mount and always begins with `.`; a category is a bare
word. They cannot collide by construction.

### Does residency retire the instancing question?

It was asked from the other end, and it deserves a direct answer:

> *"Stagecraft wants to operate part of a library, and I don't know yet if it means that it
> should instance the library more than once — that way it could have different ground rules
> from the start, including much easier path discrimination for outside tools."*

**For ground rules and path discrimination: yes, a wing is enough.** A wing whose rules differ
from the start, discriminable by path, with the library's caretaking explicitly not applying
inside it, is exactly what was described — and it costs no second instance to keep in step. That
retires the question rather than answering it, which is the better outcome.

**For storage backend: no, and nothing here should pretend otherwise.** A wing is a place inside
one store. One library on a filesystem path and one running an IPFS node are *two stores*, and
no amount of labelling inside one collapses them. If deliberate instancing survives as a real
question, that is the reason it does — see the companion petition
`how-a-library-stores-what-it-holds.md`, which is not answered here.

## The other direction: providing

The petition covered what a resident asks for. **It did not cover what the library is doing when
it answers** — and that half is this repository's, because a library cannot grant space it has
not first said it has.

So the same file is read from two ends, and the library engine is on both of them:

- **As a resident**, `.library-engine` mounted on a node asks that node for space, the same way
  `.stagecraft-engine` does. It is not privileged for being a library.
- **As a provider**, it offers the facility that other residents take up residency *in*.

**One file, two blocks.** `wants:` is the resident half and already exists. `provides:` is the
new half. Keeping them in one file is deliberate: a node reading a mounted engine's residency
learns everything about the arrangement in one read, and a provider that declared itself
somewhere else would be a second surface that can disagree with the first.

*(**Provider** is the sterile word and it is accepted here for being unambiguous. Nothing better
has turned up. If a better one does, it renames a key and costs nothing — which is worth saying
so that waiting for it never becomes a reason not to write the block.)*

## The prefix is `library`, canonically

```yaml
provides:
  - facility: library
    prefix: library
```

**Canonical, not merely default.** An outside tool looking at a node should be able to *guess*
where the library is and be right, without a lookup, without a manifest, and without asking.
That is worth more than the flexibility it costs, and the flexibility is not actually spent:
overriding the prefix is allowed and boring, and a node running two libraries obviously needs
to.

**But the real reason the key exists is the case where there is no path at all.** A library
running as an IPFS cluster has no prefix, and the honest way to say so is a declaration that
*can* carry one and doesn't:

```yaml
provides:
  - facility: library
    store: ipfs          # and no `prefix:` — the absence is the statement
```

Without the key, "not on a path" is unsayable, and a tool that assumes `library/` is a tool that
is quietly wrong about an entire class of node. **A stated intention makes a violation
visible, where an unstated one just looks like a file.**

### The store is a variable, and naming it is the point

**A library could store its contents any number of ways, and right now it knows exactly one.**
Everything assumes files unpacked into a work tree. That assumption is invisible because nothing
has ever contradicted it, which is precisely the kind of assumption worth naming before
something does.

`store:` is that name. It is not an abstraction layer and there is no driver interface behind
it. **It is a word for a thing that used to be an assumption**, and `filesystem` is the only
value anything implements.

What a second store would mean, and whether IPFS is a good first study, is asked in
`how-a-library-stores-what-it-holds.md` and is **not settled here.** That item asks for a seat,
and a seat is the right door for it — this document only makes sure the concept has somewhere to
attach when the seat exists.

## Who spawns a seat — three parties, and today they are conflated

The operator's framing, and it is the correct one: *"my entire concept of spawning in an agent
to do the advocate seats needs to be firmly framed as the library engine that's doing that —
that way it's perfectly aligned with the station node, which represents the computer workstation
and definitely owns the CPU."*

| party | owns | answers |
|---|---|---|
| `advocate.anecdote.channel` | **what a seat is** — the branch, the range, the work order, the status ladder | *how is a session prepared?* |
| `library.anecdote.channel` | **which seats exist and what they attend** — the categories, the budget, the cursor | *who gets served this round?* |
| the node — `station-node`, a civic node, a Tell | **the CPU, the clock, and the credential** | *does anything run at all?* |

Each of those is already true somewhere; none of them is written down as a boundary. The value
of writing it is that **the middle row is the one with no home**, and it has been landing by
default on whichever node happened to be running the council.

**The mechanism already exists and needs nothing new.** A station node's service runner reads
`residency.yml` out of **every** `.<name>-engine` mounted at its root — it does not carry a list
of services, precisely so there is no second list to fall out of step. An engine that serves
nothing produces nothing. So a library engine declaring a round-runner under `serves:` is how it
tells the node what it would like to run, in the vocabulary the node already reads.

And the node's discipline holds unchanged: **the claim is a menu, not a startup script.**
Declaring the runner starts nothing. Installing the job is how an operator orders from the menu,
which is why there is no `enabled: true` in a file somewhere waiting to disagree with what is
actually loaded.

### The honest gap: nothing understands a periodic service yet

A relay is a **listener** — it is up or it is down, and a health check is a socket. **A round is
periodic**: it fires, does a bounded amount of work, writes, and exits. A host that keeps a
service alive would respawn a round-runner forever.

`residency.yml` here declares `kind: periodic` anyway, and says so in the file. That is a menu
item no host can currently order from, which is legible and refusable — and *"whether the
library may refuse a label, legibly"* was already an open question on the resident side. A
declaration a host has not implemented is the same shape, seen from the provider side. It should
be petitioned for, not built around.

### What this eventually retires

A station node's council currently keeps its own registry of which local paths get a round.
Its own notes already predict the end state: *the library already enumerates everything, so a
second registry of paths is a copy that can drift* — and what the registry still holds that the
library does not is **which repositories carry seats.**

This document does not do that consolidation, and it should not be done on a guess: collapsing a
running caretaker is how a scheduled thing stops running without anybody deciding it should. But
it names the direction, and it says which side the fact belongs on when it moves.

## It is an agreement, so it is auditable

A residency states terms, so compliance is checkable by something that was not there at the
time. An auditor needs the residency files, the binding map, and a walk of the tree. **No
cooperation from the resident is required.**

Resident side:

- did the resident write **only** inside its bound labels?
- did anything marked `private` acquire a QR?
- did anything `transient` outlive its processing?
- did a wing appear for a mount that is not present?

Provider side — the new half, and the one this repository is accountable for:

- is every wing traceable to a mount that exists?
- does the declared `prefix` match where things actually are, or has the library been
  reorganised without the declaration following?
- did a seat write anywhere but its own branch?
- does anything served as `public` trace back to a label that said so?

## Open

- **May a resident nest labels?** Flat is simpler; a renderer will want `work/<pool>/…` quickly.
- **What happens to a wing when its mount is removed** — orphaned, archived, or deleted.
  `transient` versus `durable` probably already answers it per label.
- **May the library refuse a label?** It should be able to, and the refusal should be legible,
  which makes a residency a negotiation rather than a declaration.
- **Periodic services.** No host implements one. See above.
- **Two libraries on one node.** Is the second a prefix, or a second mount? The mount name is
  the claim for *residents*; nothing says what it is for *providers*, and `.library-engine`
  cannot be mounted twice.
- **Storage backends.** `how-a-library-stores-what-it-holds.md`, unanswered, and the one
  instancing case wings do not cover.
