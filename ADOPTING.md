# Adopting the constellation

`status: draft` — written 2026-09-13. **This is the deep door.** If you have been handed one of our
repositories and you do not yet know what any of it is called or why, start here and nowhere else.

It **routes**. It does not restate. Every fact below has exactly one home somewhere else, and the
link is the point — a second copy of a fact is a thing that can disagree with the first.

## Why this document is centralized, when everything else is not

Each engine has its own onboarding and each one is better than this file at its own subject. That
is not the problem this file solves.

**The problem is that you do not know our words yet.** A person arriving with a working project and
a real need cannot start at `bottles.anecdote.channel`, because nothing told them a bottle is what
they wanted. They would have to already know the answer to find the document that gives it. So the
per-engine doors are correct and they are *second*; this one is first, and its only job is to get
you to the right one having spent no more than one read.

The second reason is peer dependencies. **What you gain from an engine usually depends on what else
you have** — and no engine can honestly describe that from inside itself.

## The words, once

Seven, and they are the whole vocabulary. Nothing here is a class hierarchy; they are different
axes that happen to be spoken in the same sentence.

| word | what it is | what it is **not** |
| --- | --- | --- |
| **node** | anyone running engines. That is the entire definition. | not a server, not a tier, not something you apply for |
| **engine** | machinery a node **mounts**, as a submodule named `.<name>-engine` | not a service you call, not a package you install |
| **category** | a reserved word that names what a level of a hostname *means* — see [`CATEGORIES.md`](CATEGORIES.md) | **not an engine.** A trade site needs no trade engine |
| **pile** | the durable, encrypted-at-rest tank the bytes actually live in | not a database, not something we host for you |
| **bottle** | a subtree packed for transit — openable on a phone, with no tool but a browser | not intrinsically encrypted; sealing is a *pile* property |
| **wing** | a directory inside a library that a mounted engine owns, named by its mount | not a category; wings begin with `.` and categories never do |
| **seat** | a standing concern with a name, that wakes on a schedule and writes to its own branch | not a bot, not a reviewer with a veto |
| **grant** | a delegation of capability — somebody may now do a specific thing, usually narrow, usually expiring | **not a superuser and not an elevation.** The same word your OAuth flow already uses |

The one that surprises people: **`grant` is the plain word, not a term of art.** It can be built
up until it elevates, but that is not the mood it is delivered in — see [`GRANTS.md`](GRANTS.md).

The one people get wrong first: **a category is not an engine, and an engine is not a category.**
The axes are independent and usually do not even share a word. Do not go looking for the engine
that matches a category name.

## What adoption actually is: four gestures, and you may stop after any of them

They are cumulative in cost and **independent in commitment**. Nothing about doing one obliges you
to the next, and each is reversible except where it says otherwise.

| gesture | what you do | what it costs | reversible |
| --- | --- | --- | --- |
| **1. claim a word** | decide which reserved category your work is, and say so | nothing — a line in a file | yes |
| **2. be held** | a library points at your repository; the content stays inert | nothing, and nobody reads your bytes | yes, trivially |
| **3. mount an engine** | add `.<name>-engine` as a submodule and configure it | a pin to keep current, and a `residency.yml` to answer | yes; unmounting is a `git rm` |
| **4. take residency** | you live inside a library and keep working; you get a wing | the wing's terms, in [`RESIDENCY.md`](RESIDENCY.md) | yes, and the wing is yours until you leave |

Gestures 2–4 are the library's [three relationships](RESIDENCY.md) — *holding*, *contributing*,
*residency* — with the engine mount broken out because it is the one that costs you a pin.

**There is no fifth gesture where you join something.** There is no registry, no account, no
approval step, and nothing that has to be up for your project to work. If you ever find yourself
waiting on us for something to function, that is a bug in our design and not a step in yours.

## The roster: what each engine gives you, and what it wants first

The machine-readable form of this table — with per-row provenance, so an agent can tell a sourced
claim from a transcribed one — is [`adoption/engines.yml`](adoption/engines.yml). Read that one if
you are an agent. Read this one if you are deciding.

| engine | you gain | it becomes useful once you also have | you still have, without it |
| --- | --- | --- | --- |
| **[bottles](https://github.com/FCCN-ANTIBODY/bottles.anecdote.channel)** | a capsule that opens on a phone with no build step, and stays openable after the link that carried it dies | nothing. **Bottles is the one with no upstream.** | links, which expire, and a workaround you wrote yourself |
| **[library](https://github.com/FCCN-ANTIBODY/library.anecdote.channel)** | enumeration, admission and a clerk — the thing that says *what is here* | **bottles**, to hold bytes rather than point at them | a catalogue. Real, useful, and unable to claim custody |
| **[data-pile](https://github.com/FCCN-ANTIBODY/data-pile)** | somewhere durable and encrypted-at-rest for bottles to live | bottles worth keeping | bottles in a directory, which is fine until it is not |
| **[tell](https://github.com/FCCN-ANTIBODY/tell.anecdote.channel)** | a mailbox: submissions from people who hold nothing of yours | a **pile** to seal into, before it is configured rather than before it is mounted | whatever intake you already have, and no path for strangers |
| **[atlas](https://github.com/FCCN-ANTIBODY/atlas.anecdote.channel)** | *routability* — a directory that reports what it sees, so somebody can find you | a **tell** or a **library** worth pointing at | privacy by obscurity, which is a real choice and not a failure |
| **[advocate](https://github.com/FCCN-ANTIBODY/advocate.anecdote.channel)** | named standing concerns that wake up, think, and open pull requests | nothing. It runs from a terminal with no host anywhere. | a maintenance backlog that only exists while somebody remembers it |
| **[judgement](https://github.com/FCCN-ANTIBODY/judgement)** | a summonable admission step: `accept` / `reject` / `needs-judgment` | something that admits things — a **tell**, usually | your own admission rule, written where you can read it |
| **[journal](https://github.com/FCCN-ANTIBODY/journal.anecdote.channel)** | content-less Jekyll machinery for a public record, and the conventions with it | a site you were going to build anyway | your own Jekyll, which is probably working |
| **[antidote](https://github.com/FCCN-ANTIBODY/antidote)** | the archivist: intake, plaque index, custody ledger, egress | a custody claim somebody might audit | nothing you are currently missing. Skeleton status |
| **[anecdote.channel](https://github.com/FCCN-ANTIBODY/anecdote.channel)** | the offline origin, and the shared instruments the rest is built from | nothing; it is standalone and it is where capability moves *to* | the engines, which increasingly defer to it |

Two outside the org, mounted the same way and adopted the same way:
**[stagecraft](https://github.com/DiscoveryWritten/stagecraft)** (a render relay — a second machine
draws frames for yours) and **proofing** (capture and proof sheets). Same `.<name>-engine`
convention, same `residency.yml`, no special status.

### The rule that makes this table readable

**A dependency of a verb is not a dependency of a product.** Stagecraft wrote it down first and it
governs everything above: a station that never renders remotely never starts a relay and is never
told off about it. So when the roster says an engine "becomes useful once you also have" something,
that is a statement about **one capability**, never about whether the engine will function.

This is why our peer dependencies are declared **per verb**, and why every declaration carries a
mandatory `without:` key saying what you still have if you never adopt the peer. The schema, and
the reasoning it was built with, is [`PEERS.md`](PEERS.md).

## The `-enough` family — the smallest thing to adopt, and the easiest to miss

Not engines. **Instruments** — libraries you import, not machinery you mount. They are listed
separately because they are adopted differently and because nothing about the engine roster would
lead you to them.

**The suffix is a promise, and it is the naming convention doing deliberate work.** A member is
*enough of that tool to do the work here, with nothing installed*:

> The real tool needs a machine. These need a tab.

That makes the membership test mechanical rather than a matter of taste, and `jekyll-enough` ships
it as a suite:

> **Healthy:** the modules import each other and nothing else. Not a package, not a `node:`
> builtin, not a file outside the repository.
>
> **Failed:** it acquired a dependency that only exists on a workstation, and nothing said so.

**The thing that ends a member is not a bad feature — it is an import.** A module that quietly
starts needing a package or a real filesystem has stopped being an `-enough` tool while keeping the
name, and that failure is invisible from inside its own repository. Which is why it lives in a test
and not in a README.

### Why this matters to an adopter more than the engines do

If your project has ever written *no frameworks* or *no third-party vendors in the runtime* in its
own README, **this family is the part of the constellation you already agree with**, and it is
adoptable without adopting anything else. There is no mount, no residency, no category to claim —
`import` it, or do not.

### The members, and what state each is actually in

| instrument | gives you | state |
| --- | --- | --- |
| **[`jekyll-enough`](https://github.com/FCCN-ANTIBODY/jekyll-enough)** | a Jekyll build — front matter, Liquid, `_data`, permalinks — over an in-memory `path → content` map | **its own repo.** The first member to get an address |
| **`git-enough`** | the push. A git client that speaks send-pack from a tab | built, inside `anecdote.channel` |
| **`qr-enough`** | a vendorless byte-mode QR encoder, verified scannable against real decoders | built, inside `anecdote.channel` |
| **`seal-enough`** | the encryption factory — pile crypto that is **almost entirely WebCrypto-native** | designed, decided, not built |
| **`actions-enough`** | the workflows: running a CI definition without a runner | designed, measured |
| **`sh-enough`** | a shell interpreter | **new work, not an extraction.** Measured and warned about, not planned |
| `yaml-enough`, `cron-enough`, `node-enough`, `liquid-enough` | — | intended |

**`seal-enough` is the one worth knowing about**, because it is where the constellation's cryptography
meets the tab. Every step of the pile's crypto core has a WebCrypto answer — the ratchet, the key
commitment, the IV, AES-256-CTR, the entries digest, the Ed25519 signed head — **except one**: the
`age` seed-wrap, because `subtle` has X25519 but not ChaCha20-Poly1305.

The resolution is worth copying rather than re-deriving, and it is the kind of thing this primer
exists to hand over: **native-local at rest, `age` synthesized only on export.** A pile that stays
yours needs no `age` at all; `age` is needed only at the handoff boundary, where an existing verifier
expects an age-wrapped seed. The gap was real and it turned out not to be monolithic.

## Choosing, in the order the questions actually bite

1. **What word are you?** Pick from [`CATEGORIES.md`](CATEGORIES.md). It costs nothing, it is a line
   in a file, and it is the only decision that gets *harder* to change later — because a word taken
   back is a migration, and the person who pays is whoever federated with you in between.
   The per-word doors are in [`adoption/`](adoption/); [`trade`](adoption/trade.md) is written.
2. **Is anything of yours dying on a clock?** Expiring URLs, a CDN with signed links, a host you do
   not control. If yes, **bottles** is your first engine and everything else can wait.
3. **Do you already enumerate what you have?** If your project has an index, a catalogue, or a
   listing page, you have most of a **library** and did not know it.
4. **Does anyone need to reach you who holds nothing of yours?** That is a **tell**, and it is the
   only answer to that question we have.
5. **Do you want to be findable?** Only then, an **atlas**. Discoverable and joinable are different
   decisions, and a publicly discoverable mailbox delivering to insiders only is coherent.
6. **Is there a concern here nobody has time for?** Seat an **advocate**. It is the cheapest thing
   on the list and the only one that costs no runtime at all.

**You are allowed to answer 2–6 later.** They were written in this order because that is the order
they hurt, not because a step is owed before the next one is permitted.

## What we will not ask of you

These are load-bearing and each is easy to lose by accident, which is why they are written as
refusals rather than as values:

- **No library card.** Checking a bottle out, editing it, and putting it back requires nothing from
  our software. If lending ever depends on us being up, reachable, or asked first, we broke it.
- **No front desk.** Nothing central decides whether a change to your artifact is allowed.
- **Honest defaults fire nothing.** Judges, thresholds and automation ship *off*. A mounted engine
  starts nothing; the claim in a `residency.yml` is a menu, not a startup script.
- **Everything must stay runnable by hand.** The moment a thing only runs when a node starts it,
  the node has become a dependency.
- **Witness, not judge.** A submission is never blocked; the submitter learns the outcome instead.
- **Verify-from-anyone.** Trust decides *action*, not *admission*.

The full list is the invariants in
[`civic-node/AGENTS.md`](https://github.com/FCCN-ANTIBODY/civic-node/blob/main/AGENTS.md), and the
one that governs the rest: **replication is the test.** Could the next operator copy this and
understand what they copied? If adopting us made that harder for you, we would rather hear it.

## The worked examples

Fitting a real project is the only way this document gets better, so the fittings are published
rather than kept:

- **[artist-lockers](adoption/worked/artist-lockers.md)** — a Discord-sourced media catalogue on
  GitHub Pages, with an IPFS pinning layer it had to build itself. The first fitting, and the
  reason the `trade` health row says *nobody is wedged into a workaround by a gap in our tools*.

## Where to go after this

| your question | the one file |
| --- | --- |
| Which reserved word am I? | [`CATEGORIES.md`](CATEGORIES.md) |
| What does my word owe, and what does it get? | [`adoption/`](adoption/) — one door per word |
| How do I declare a peer dependency? | [`PEERS.md`](PEERS.md) |
| What does the `-enough` suffix promise? | [`jekyll-enough`](https://github.com/FCCN-ANTIBODY/jekyll-enough)'s `dependencies.test.mjs` |
| What does living inside a library mean? | [`RESIDENCY.md`](RESIDENCY.md) |
| Why is the README the front page, and how do I write one? | [`EXHIBIT.md`](EXHIBIT.md) |
| What does a library need from a bottle? | [`BOTTLES.md`](BOTTLES.md) |
| Who speaks for a standing concern, and how? | [`SEATS.md`](SEATS.md) |
| What is still unsolved here? | [`OPEN.md`](OPEN.md) |
| What is unsolved constellation-wide? | [`civic-node/OPEN-QUESTIONS.md`](https://github.com/FCCN-ANTIBODY/civic-node/blob/main/OPEN-QUESTIONS.md) |
| Why was a cross-cutting thing decided that way? | [`anecdote.channel/docs/decisions.md`](https://github.com/FCCN-ANTIBODY/anecdote.channel/blob/main/docs/decisions.md) |

---

**This file lives in the library because enumeration is what a library is for**, and a roster of
engines is an enumeration. It is not a claim to speak for the engines: every row above is sourced,
and the moment an engine declares its own peers in its own `residency.yml`, the row here is
regenerated from it and the transcription is deleted. That retirement rule is the whole reason a
central roster is allowed to exist at all — see [`PEERS.md`](PEERS.md), "the second surface".
