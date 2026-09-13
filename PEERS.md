# Peer dependencies — the `peers:` block, and why it is per-verb

`status: draft` — written 2026-09-13. **This document is the referee for a block in
`residency.yml`.** It is the same act [`RESIDENCY.md`](RESIDENCY.md) performed for `wants:` and
`serves:`: a producer contract needs a referee, or it is written down on one side only.

## The problem, stated precisely

Everything in this constellation is technically a **peer** dependency. Nothing bundles anything;
engines are submodules a node mounts, and any two of them are siblings under one root. So saying
*"they are all peer dependencies"* is true and useless — it does not answer the only question an
adopter actually has, which is:

> **If I take this one and not that one, what do I get, and what silently does not work?**

The two failure modes are symmetrical and both are common:

- **A dependency stated too strongly** makes an adopter take four repositories to get one
  capability, and they are right to walk away.
- **A dependency not stated at all** makes them adopt something that appears to work, and
  discover a year later that the part they cared about was never doing anything.

## The answer: a dependency of a verb is not a dependency of a product

`.stagecraft-engine/residency.yml` wrote this first, about services:

> *A station that never wants remote rendering never starts a relay and is never told off about
> it — the same per-verb rule the peer idiom already uses, where a dependency of a verb is not a
> dependency of a product.*

**Peer dependencies inherit that rule verbatim.** A `peers:` entry never says *this engine needs
that engine*. It says **which of this engine's verbs stop working**, and — mandatorily — what you
still have when they do.

The library is the clean example and the reason this block was written:

- The library does **not** need bottles to run. Mount it with nothing else and it enumerates.
- But *holding* — the custody claim, *this library has it and has had it since then* — requires
  the bytes, and the bytes live in bottles.
- So the honest declaration is not "requires bottles." It is: **`for: [holding, custody]`,
  `without:` a catalogue.** A catalogue is a real thing that is useful to real people. Saying so
  is not a hedge; it is the fact an adopter is choosing between.

## The schema

A top-level `peers:` list in an engine's `residency.yml`, alongside `wants:`, `provides:`,
`serves:` and `ejects:`. Flat dicts only — scalars, quoted strings, and `[flow, lists]` — because
the readers that consume residency files are deliberately small parsers rather than a YAML
library, and putting a package manager in a node's boot path is not a trade anyone here wants.

```yaml
peers:
  - peer: bottles                                  # the engine's short name, never a path
    repo: FCCN-ANTIBODY/bottles.anecdote.channel   # unambiguous; short names are for humans
    strength: optional                             # required | optional | vendored
    for: [holding, custody]                        # THE VERBS. Never the product.
    without: "a catalogue: it can point at things, it cannot claim to hold them"
    mount: none                                    # none | .bottles-engine | vendored
    source: "README.md#holding-and-the-bytes-it-does-not-have"
```

### Every key, and what it is for

| key | required | what it means |
| --- | --- | --- |
| `peer` | yes | short name. The word a person says. Not a path and not a URL |
| `repo` | yes | `org/name`. Short names collide across orgs eventually; this does not |
| `strength` | yes | one of three, below |
| `for` | yes | the verbs of **this** engine that the peer is a dependency of. Never empty — an entry with no verb is not a dependency, it is a mention |
| `without` | **yes** | what an adopter still has if they never take the peer. The load-bearing key |
| `mount` | yes | `none` if the peer need not be mounted; a `.<name>-engine` path if it must; `vendored` if this engine already mounts it for you |
| `source` | yes | where in this repository the claim is argued. A peer entry with no argument behind it is a guess |

### `strength`, and only three values

| value | means | the adopter's question it answers |
| --- | --- | --- |
| `required` | the engine does not function without it. `for:` lists every verb, and `without:` says *nothing* | "can I skip it?" — no |
| `optional` | named verbs stop; the rest of the engine is unaffected | "what do I lose?" — exactly `for:`, and you keep `without:` |
| `vendored` | **this engine already mounts it.** You get it by mounting this one, and you do not mount it yourself | "is this a second thing I have to adopt?" — no |

`vendored` is the value most likely to be left out, and leaving it out is expensive: an adopter who
does not know an engine is already inside will mount a second copy at a second pin, and the two
will drift. The library vendors the advocate engine. Tell vendors judgement. Both are invisible
from a `.gitmodules` at the node root, which is exactly why they have to be said.

### Why `without:` is mandatory and cannot be empty

Because it is the only key that cannot be written dishonestly by accident.

`strength: optional` costs nothing to type and tells an adopter almost nothing. Being made to
finish the sentence — *without bottles, this is a catalogue* — forces whoever writes the entry to
know whether the degraded thing is still worth having. **If the `without:` reads as a description
of something broken, the strength was wrong and it should have said `required`.** That is the
review question for every entry in this file, and it is the whole reason the key exists.

For `strength: required`, `without:` is the literal string `nothing` plus what does not happen. It
is still not optional to write.

## What a `peers:` block may not do

- **It may not name a consumer.** An engine describes the capability, never the customer. A peer
  entry that only makes sense because one known adopter needs it is configuration, not a peer.
- **It may not declare on someone else's behalf.** An engine says what *it* wants. It never
  declares what the peer requires back — that is the peer's own file, and two files asserting one
  relationship is a disagreement waiting to be discovered by whoever federated with both.
- **It may not start anything.** Same rule as the rest of the residency claim: **the claim is a
  menu, not a startup script.** A `required` peer that is absent produces a legible refusal when a
  verb is attempted, never a failure at mount time.
- **It may not be transitive.** Neighbors, not a graph. Declare the peers you touch; do not
  enumerate theirs. An adopter walks the graph one hop at a time, on purpose.

## The second surface, and the retirement rule

[`adoption/engines.yml`](adoption/engines.yml) is a **central roster** of every engine and its
peers, and a central roster is precisely the thing `residency.yml` warns against:

> *A provider declaring itself somewhere else would be a second surface that can disagree with
> the first.*

That warning is correct and the roster still has to exist, because the adopter this whole effort
is for is the one who cannot yet clone eleven repositories to find out what they are called. So
the roster is allowed under three conditions, and it is not allowed without them:

1. **Every row carries `declared:`.** Either a path to the engine's own `residency.yml` — meaning
   the row was read from the engine and the engine owns it — or the literal `transcribed`, meaning
   a human read that engine's prose and wrote this down. A reader can always tell which.
2. **`transcribed` is a debt with a name.** It is not a permanent state and it is not equivalent
   to a declaration. Every transcribed row is a small owed pull request against that engine.
3. **The transcription is deleted on the day it is replaced.** When an engine ships its own
   `peers:` block, the roster row is regenerated from it, `declared:` changes to the path, and the
   hand-written text goes. **Not kept as a fallback** — a stale fallback that agrees with nothing
   is worse than an absent row, because an absent row is visibly absent.

This mirrors the library's own rule about its catalogue: generated from what is visible, never
from what a held project says about itself. The roster is a catalogue of engines, and it is held
to the same standard it holds everything else to.

## Where this leaves the engines today

**One engine declares its peers: this one.** Every other row in the roster is `transcribed`, which
means this document currently describes a convention with a single implementation. That is
recorded honestly rather than smoothed over — see [`OPEN.md` §9](OPEN.md), which asks the question
this design cannot answer from inside the library: whether `peers:` belongs in `residency.yml` at
all, or whether residency and peerage are two axes that have been conflated because they happened
to arrive in the same file.
