# Fitting: artist-lockers

`status: draft` — fitted 2026-09-13 against [`tiliv/artist-lockers`](https://github.com/tiliv/artist-lockers)
at `3f68225`. **The first white-glove fitting**, published whole rather than as its conclusion.

**Nothing here was asked of them.** The project was read; this is what an adoption *would* look
like, with the reasoning attached so they can disagree with it in specifics rather than in
general. Every recommendation names what it costs and what it closes.

## What the project is

A **Discord-sourced media catalogue that publishes itself as a static site.** A `discord.py` bot
wakes long enough to read messages since its last appearance, keeps only those carrying a media
signal — attachment, embed, or a link to a supported music domain — and commits what it found to
`_data/<guild>/<category>/refs.json`. Jekyll builds that into a site; GitHub Pages serves it;
Cloudflare caches it. Its own vocabulary: a **Locker** is a Discord category, a **Channel** is a
text channel or forum post, an **Author** is whoever posted inside one.

It is a **template repository** — the first line of its README tells you to copy it and be
detached from upstream, "which you should consider a feature."

Its stated philosophy, verbatim in places, because three lines of it are load-bearing below:

> *No third-party vendor support loaded by the frontend runtime.*
> *Accumulate offline media caches.*
> *All monolith entry points are offered by `bin/` executables.*

## Why this project first

Because we did not choose it for being a good fit. **It is a good fit, and it also already built
one of our engines by itself** — which is the failure the `trade` health row names, caught for the
first time in the act:

> *nobody is wedged into a workaround by a gap in **our** tools.*

`bot/cdn.py` parses the signed query parameters on a Discord CDN attachment URL — `ex`, `is`, `hm`
— and computes the expiry. They know, precisely and in code, that the links they catalogue die on
a clock. So `bin/pin --budget N` and `bin/distribute.mjs` push the bytes to IPFS through Pinata,
under a budget, to survive it.

That is a **custody layer**, built from scratch, by a project that had no idea we had a word for
it. It is a correct engineering decision and it was invisible to us until somebody read the repo.
See [`../trade.md`](../trade.md), "the wedge".

## The words they would claim

Two answers, and the fact that it is two is the first thing this fitting taught us.

| what | word | why |
| --- | --- | --- |
| the repository — a template other people copy to run their own | **`trade`** | business, money or not. A tool that other parties adopt is trade, and *the template still builds* is one of its health rules |
| what it holds and serves — music, art, attachments | **`media`** | the health rule is that the artifact still **plays**, and that is a different clock from the repo's |
| the **authors** in it | see below | this is the part that does not fit cleanly, and it is the honest finding |

**The health rules genuinely differ, which is why this is not pedantry.** A Jekyll build breaking
is noticed the same afternoon. A container nothing decodes any more is noticed in ten years by
somebody who is not them. Their `bin/pin` budget guards the second and nothing guards the first.

### And the part that does not fit: the authors

`media` says healthy means *it still plays*. `voices` says healthy means *attribution is intact and
the writer can still withdraw*. An artist who posted a track into a Discord Locker is plainly
covered by both, and the project has neither rule written down: entries are keyed on a Discord
message id, and **there is no withdrawal path** — not because anyone refused one, but because the
question has not been posed.

We do not have an answer for them. **A project holds more than one category's worth of obligation
and our reserved words are per-hostname-level**, so there is nowhere for it to say so. That is
recorded as [`../../OPEN.md` §10](../../OPEN.md) and it came out of this fitting.

## Where their philosophy and ours already agree

Worth saying before any recommendation, because it is the reason the fit is close and it means
most of the work is naming, not building:

| their line | our name for it |
| --- | --- |
| *no third-party vendor support loaded by the frontend runtime* | **a player that needs no build step** — [`../../BOTTLES.md`](../../BOTTLES.md) §1.2 |
| *accumulate offline media caches* | **the caching role** — serving captures when the web is down, [`../../BOTTLES.md`](../../BOTTLES.md) §3 |
| *all monolith entry points are offered by `bin/` executables* | **everything must stay runnable by hand.** The moment a thing only runs when a host starts it, the host has become a dependency |
| *messages and media are treated as stable once fetched* | **the carbonite property** — a frozen capsule is why custody is provable, [`../../BOTTLES.md`](../../BOTTLES.md) §2 |
| *you should consider being detached from my updates a feature* | **replication is the test.** Could the next operator copy this and understand what they copied |

Four independent arrivals at the same four positions. That is not a coincidence worth flattering
anybody with — it is evidence the positions are forced by the problem, which is the strongest form
of agreement available.

## What we would suggest, in the order it hurts them

### 1. Bottles — because their clock is already running

Their pain, in their code, today. `bin/pin` is a budget against link death and Pinata is a
**gateway** — a third-party vendor in the durability path, which their own philosophy dislikes
everywhere except here, where they had no alternative.

What a bottle changes: the artifact carries its own manifest and opens with a browser and nothing
else. No gateway to be up, no pin to keep paid, no CID to resolve through somebody. Their offline
media cache stops being a cache and becomes the artifact.

**And bottles is `draft`.** The vocabulary is settled; the wire format is not. So the honest
recommendation is *not* "adopt bottles":

> **Do not remove Pinata. Do not wait for us.** Keep pinning. What is worth doing today is one
> commit: make the bottle-shaped seam explicit — one function that answers *where do the bytes for
> this ref live*, with Pinata behind it — so that adopting bottles later is a swap and not a
> rewrite of every stored reference. That costs them an afternoon and it is the whole of the
> now-decision in [`../trade.md`](../trade.md).

### 2. An advocate seat — because it is free and their first one writes itself

No listener, no runtime, no service, runnable from a terminal. It wakes, does a bounded amount of
work, writes to its own branch, and opens a pull request.

Their first seat is already implied by their own code: **`bot/cdn.py` can compute an expiry, and
nothing reads it in aggregate.** A seat that walks `refs.json`, counts how many references are past
`ex` or close to it, and opens a pull request saying so, turns a known-in-principle decay into a
number somebody sees on a schedule. That is the cheapest real thing on this page.

### 3. Library — because they already are one and did not know

*A library is already listing what is inside it, because that is what a library is.* `refs.json` is
an enumeration. The site is its rendering. They have the hard half.

Two shapes, and the choice is theirs:

- **Be held.** A library points at their repository; the content stays inert; nobody reads their
  bytes. Costs nothing, reversible, and gets their enumeration into an index others can plug into.
- **Be one.** Mount `.library-engine` and their catalogue becomes federatable — an Atlas plugged
  into it gets the whole index on tap, instead of having to go and crawl for it.

**Their Discord auth is fine, and this is the case that makes the rule concrete.** Their
Cloudflare Worker (`worker/discord-auth.js`) authenticates site visitors against Discord. Our rule
is *no library card* — nothing central may decide whether a change is allowed, and a card may
never be a prerequisite. Theirs is not one, and the library README already blesses it: *a library
card is an establishment's local concern, for their own metrics. Legitimate, and theirs.* The one
line to hold: **an artifact must remain openable by somebody who never authenticated.** Gate the
comfortable path, never the bytes.

### 4. Tell — because Discord is currently the only door

Everything enters through a Discord message in a category the bot watches. That is a good intake
and it is a **membership** intake: to give them something you must already be in the server.

A Tell is a mailbox for people who hold nothing of theirs. It is inert until spoken to, it needs
no origin anywhere, and it does not oblige them to accept anything — *witness, not judge*; a
submission is never blocked, the submitter learns the outcome instead.

Not urgent. Named because *"there is no way in without a Discord account"* is a decision they
should make on purpose rather than inherit from their bot.

### 5. Atlas — deliberately last

Routability, once there is something worth pointing at. **Discoverable is not joinable**, and a
publicly discoverable catalogue that admits nobody is a coherent thing. Reversible, and there is
no reason to think about it this year.

### What we would not suggest

- **stagecraft** — a render relay. They do not render; nothing to gain.
- **journal** — content-less Jekyll machinery. They have working Jekyll with their own `_plugins`,
  and *"your own Jekyll, which is probably working"* is the honest `without:`. Adopting it would be
  a rewrite in exchange for conventions they have already independently arrived at.
- **civic-node, antidote** — no jurisdiction, and a skeleton respectively.
- **judgement** — they have a media-signal admission rule already, in code they can read. A judge
  ships off and would start as a slower way to do what a regex does. Revisit only if admission
  becomes contested.

## Their decision ledger

| decide now | why now |
| --- | --- |
| the words: `trade` for the repo, `media` for the holdings | a line in a file today; a migration once anyone federates with them |
| the addressing seam — one function answering *where do these bytes live* | they are mid-flight on a pinning layer. Retrofitting content-addressing means rewriting every stored reference |
| whether Discord auth is a convenience or a prerequisite | it is a convenience today, by accident. Making it load-bearing is easy and expensive to undo |

| decide later | it will still be cheap |
| --- | --- |
| every mount | `git submodule add` in, `git rm` out |
| bottles adoption | the seam above is what buys the option; the swap can wait for `draft` to end |
| held vs. being a library | both reversible, and doing one first does not spend the other |
| a Tell, an Atlas, more seats | independently adoptable, in any order, none obliging the next |
| running anything at all | a mounted engine starts nothing. **The claim is a menu, not a startup script** |

## What this fitting taught us

The point of publishing the fitting rather than the conclusion. Five findings, and two are
uncomfortable:

1. **They needed a door before they needed a repository.** Nothing in this project would have led
   anyone to `bottles.anecdote.channel` — you would have to already know a bottle was the answer to
   find the document that gives it. This is the argument for a centralized entry point stated as
   evidence instead of as an opinion. [`../../ADOPTING.md`](../../ADOPTING.md) exists because of it.

2. **The wedge was found by reading their code, not by them reporting it.** Nobody was withholding
   anything; from inside their project nothing is wrong, because a custody layer *is* the right
   thing to build when there is no other. Our only current discovery mechanism is *somebody reads
   your repository*, and that scales to roughly one adopter. Named in
   [`../trade.md`](../trade.md); no mechanism proposed, because we do not have one.

3. **Ranking by pain inverted our architecture, and the inversion is right.** Read
   bottom-up — origin, engines, categories — bottles is deep infrastructure. Read from their
   problem, it is the first thing and everything else can wait years. Every door in
   [`../`](../) should rank by pain, and the roster ordering in `ADOPTING.md` is for orientation
   only.

4. **Ranking by pain points at our least-finished work, and it will keep doing that.** Their
   top-ranked engine is `draft`. That is not a scheduling accident: the gaps that hurt adopters
   most are the gaps we have not closed. So an onboarding document has to be able to say *this is
   the right answer and it is not ready*, and to give a useful now-move anyway — which is why the
   bottles recommendation is a seam and not an adoption.

5. **One project holds more than one category's worth of obligation, and cannot say so.** `trade`
   repo, `media` holdings, `voices`-shaped consent duties toward the artists in it. Our reserved
   words occupy a level of a hostname; this project needs three of them at once and has nowhere to
   write that down. [`../../OPEN.md` §10](../../OPEN.md).
