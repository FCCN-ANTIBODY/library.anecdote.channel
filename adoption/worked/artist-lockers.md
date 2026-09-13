# Fitting: artist-lockers

`status: draft` — **second pass**, revised 2026-09-13 against
[`DiscoveryWritten/artist-lockers`](https://github.com/DiscoveryWritten/artist-lockers) at `3f68225`
(then at `tiliv/artist-lockers`, which now redirects), the same commit the
first pass read. Nothing in the project changed. What changed is that this pass sorted it by
**what has to be running when somebody opens the page**, and three claims from the first pass did
not survive that.

> **This file is disposable, on purpose.** Everything transferable from it lives in
> [`../README.md`](../README.md), "how to run a fitting" — nine rules, each paid for by something
> this fitting got wrong first. What stays here is the reading of *one project at one commit*, and
> that has an expiry: once they have onboarded, keeping a public reading of somebody's repository is
> a courtesy nobody asked for. **Deleting it should cost nothing, and it does.**

**Nothing here was asked of them.** The project was read; this is what an adoption *would* look
like, with the reasoning attached so they can disagree with it in specifics rather than in general.
Every recommendation names what it costs and what it closes.

## What the project is

A **Discord-sourced media catalogue that publishes itself as a static site.** A `discord.py` bot
wakes long enough to read messages since its last appearance, keeps only those carrying a media
signal — attachment, embed, or a link to a supported music domain — and commits what it found to
`_data/<guild>/<category>/refs.json`. Jekyll builds that into a site; GitHub Pages serves it;
Cloudflare caches it. Its own vocabulary: a **Locker** is a Discord category, a **Channel** is a
text channel or forum post, an **Author** is whoever posted inside one.

It is a **template repository** — the first line of its README tells you to copy it and be detached
from upstream, "which you should consider a feature."

## The line they already drew

The first pass treated *static* as one property among several. It is not. It is the spine, and the
project states it in configuration rather than in prose. `_config.yml`:

```yaml
exclude:
  - CNAME
  - README.md
  - Gemfile
  - vendor
  - bot
  - bin
  - worker
  - node_modules
  - __pycache__
  - package.json
  - ".*"
  - "*.toml"
  - "*.yaml"
  - "*.lock"
```

**Every executable thing in the repository is excluded from the thing the repository publishes.**
The bot, the entry points, the worker, all three package manifests, every lockfile. What survives
into `_site` is HTML, CSS, three JavaScript modules, and `_data`.

That is not a build detail. It is the project drawing the artifact/apparatus line itself, in a file,
and it is a sharper line than we drew for them. So this pass adopts it as the sort:

| | what is in it | must it be alive when a reader opens the page |
| --- | --- | --- |
| **apparatus** | `bot/`, `bin/`, `worker/`, Jekyll, the four toolchains | **no.** It ran before publication or it did not run |
| **the artifact** | `index.html` with every ref inlined, `_data/**/refs.json`, `css/`, `js/`, the OPFS cache | **it is the bytes.** Nothing to be alive |
| **read-time dependencies** | `cdn.discordapp.com`, the Pinata gateway, `discord.com` | **yes — and this is the whole of the exposure** |

Everything below ranks by that third row, because it is the only row where a third party can take
something away from them.

## What the first pass got wrong

Stated first, because two of the three were recommendations to build things they have.

### 1. The Cloudflare Worker is not in the runtime path. It is vestigial.

The first pass said *"Their Cloudflare Worker (`worker/discord-auth.js`) authenticates site
visitors against Discord."* It does not, at this commit.

`js/discord-auth.js` is a **public-client PKCE flow**. It generates a verifier, redirects to
Discord, and exchanges the code by POSTing `https://discord.com/api/oauth2/token` **directly from
the browser** — no client secret, no intermediary. The worker is a confidential-client exchange
that nothing calls. Three independent signs it is dead:

- nothing under `js/`, `_includes/`, or `index.html` references a worker URL;
- `worker/wrangler.toml` still carries the template placeholder
  `REDIRECT_URI = "https://yourdomain.com/auth/callback"`;
- its CORS header is hardcoded to `https://tiliv.github.io`, the upstream author's Pages origin,
  which is wrong for every copy of a template repository.

**This is a correction in their favour and it is the most static thing about the project.** They
already removed the server from the auth path; PKCE is precisely the flow that lets a static site
authenticate with no backend. The residue is one of the four toolchains, and deleting
`worker/`, `bin/deploy-discord-auth`, and the wrangler dependency **takes the floor from four
toolchains to three at no cost.** That is the cheapest item in this document and it did not appear
in the first pass at all.

### 2. `acquireBlob()` is already the seam we told them to spend an afternoon building

The first pass's headline now-move was *"one function that answers where do the bytes for this ref
live, with Pinata behind it."* That function is `js/player.js`, it is called `acquireBlob`, and it
has three tiers:

1. **OPFS** — `navigator.storage.getDirectory()`, a local file keyed by message id. No network.
2. **Pinata** — a `fetch` of ``https://{{ site.pinata_gateway }}/ipfs/${record.cid}``
   (`js/player.js:64`), then write the bytes into OPFS on the way past.
3. **The Discord CDN**, with their own comment: `// this is will not work after the cdn url's
   expiration`.

Tier 1 before tier 2 before tier 3, cheapest and most durable first. **The architecture is already
right.** The remaining gap is one line, not an afternoon: the vendor hostname is Liquid-templated
into the JavaScript at build time, so *which* gateway is a rebuild rather than a value. Adopting
bottles later means adding a tier to a function that already takes tiers.

### 3. The auth gate cannot be a prerequisite, and this is structural rather than a choice

The first pass listed *"whether Discord auth is a convenience or a prerequisite"* as something for
them to decide, and hoped they would keep it a convenience. They cannot make it anything else
without ceasing to be a static site.

`index.html` loops `site.data` unconditionally and emits every link — CDN URL, IPFS CID, label,
deep link — into `data-player` attributes at build time. `_includes/auth.html` is an overlay;
`js/unlocker.js` sets `display: none` on it when Discord returns a matching guild. **The bytes are
delivered before the gate is drawn, to everyone, always.** View-source is the bypass.

Our rule — *an artifact must remain openable by somebody who never authenticated* — is therefore
satisfied by construction. We record that as compliance, and simultaneously as the one thing on
this page they might not know: **a static host cannot gate, it can only decorate.** If the gate is
meant to be load-bearing, the fix is not a better gate, it is leaving GitHub Pages, and that trade
should be made deliberately rather than discovered.

## Why this project first

Because we did not choose it for being a good fit. **It is a good fit, and it also already built
one of our engines by itself** — which is the failure the `trade` health row names, caught for the
first time in the act:

> *nobody is wedged into a workaround by a gap in **our** tools.*

`bot/cdn.py` parses the signed query parameters on a Discord CDN attachment URL — `ex`, `is`, `hm`
— and computes the expiry. They know, precisely and in code, that the links they catalogue die on a
clock. So `bin/pin --budget N` and `bin/distribute.mjs` push the bytes to IPFS through Pinata, under
a budget, to survive it.

That is a **custody layer**, built from scratch, by a project that had no idea we had a word for it.
It is a correct engineering decision and it was invisible to us until somebody read the repo. See
[`../trade.md`](../trade.md), "the wedge".

## The words they would claim

Two answers, and the fact that it is two is the first thing this fitting taught us.

| what | word | why |
| --- | --- | --- |
| the repository — a template other people copy to run their own | **`trade`** | business, money or not. A tool that other parties adopt is trade, and *the template still builds* is one of its health rules |
| what it holds and serves — music, art, attachments | **`media`** | the health rule is that the artifact still **plays**, and that is a different clock from the repo's |
| the **authors** in it | see below | this is the part that does not fit cleanly, and it is the honest finding |

**The health rules genuinely differ, which is why this is not pedantry.** A Jekyll build breaking is
noticed the same afternoon. A container nothing decodes any more is noticed in ten years by somebody
who is not them. Their `bin/pin` budget guards the second and nothing guards the first.

### And the part that does not fit: the authors

`media` says healthy means *it still plays*. `voices` says healthy means *attribution is intact and
the writer can still withdraw*. An artist who posted a track into a Discord Locker is plainly
covered by both, and the project has neither rule written down: entries are keyed on a Discord
message id, and **there is no withdrawal path** — not because anyone refused one, but because the
question has not been posed.

The static framing makes this worse in a way worth stating plainly. Withdrawal from a static site is
a rebuild — fine, they rebuild on every push. But withdrawal from **OPFS is impossible**: those
bytes are in a stranger's browser profile, and no rebuild reaches them. Any withdrawal promise this
project could make has a boundary at the reader's disk, and that boundary is a property of being
static, not a failure of care.

We do not have an answer for them. **A project holds more than one category's worth of obligation
and our reserved words are per-hostname-level**, so there is nowhere for it to say so. That is
recorded as [`../../OPEN.md` §10](../../OPEN.md) and it came out of this fitting.

## Where their philosophy and ours already agree

Worth saying before any recommendation, because it is the reason the fit is close and it means most
of the work is naming, not building:

| their line | our name for it |
| --- | --- |
| *no third-party vendor support loaded by the frontend runtime* | **a player that needs no build step** — [`../../BOTTLES.md`](../../BOTTLES.md) §1.2 |
| *accumulate offline media caches* | **the caching role** — serving captures when the web is down, [`../../BOTTLES.md`](../../BOTTLES.md) §3 |
| *all monolith entry points are offered by `bin/` executables* | **everything must stay runnable by hand.** The moment a thing only runs when a host starts it, the host has become a dependency |
| *messages and media are treated as stable once fetched* | **the carbonite property** — a frozen capsule is why custody is provable, [`../../BOTTLES.md`](../../BOTTLES.md) §2 |
| *you should consider being detached from my updates a feature* | **replication is the test.** Could the next operator copy this and understand what they copied |
| *no frameworks* | **the `-enough` family.** Enough of a tool to do the work here, with nothing installed — and an import is what ends a member, tested as a suite |

Five independent arrivals at the same five positions. That is not a coincidence worth flattering
anybody with — it is evidence the positions are forced by the problem, which is the strongest form
of agreement available.

### The first line is the one they are currently breaking

*No third-party vendor support loaded by the frontend runtime* is in their README. `js/player.js`
line 64, in the frontend runtime, is a `fetch` to a Pinata gateway.

**This is not a gotcha and it is not hypocrisy — it is the absence of an alternative**, which is
exactly what a wedge is. They needed durable bytes, durable bytes needed a CID, and a CID in a
browser needs somebody's gateway. Every other vendor was designed out of the runtime; this one
survived because nothing else was on offer. It is the single strongest argument for bottles on this
page, and they wrote it themselves as a rule they then had to break.

### The toolchain bill is real, and it is entirely apparatus

*No frameworks* is in their README. **Building this static site requires four toolchains**: Ruby
with bundler (`Gemfile`, `.ruby-version`), Python with uv (`pyproject.toml`, `.python-version`),
Node (`package.json`, `yarn.lock`), and Cloudflare's wrangler for the auth worker. Each is
defensible on its own and the total is not what anybody chose.

The static framing sharpens the number in both directions:

- **None of it reaches a reader.** All four are excluded in `_config.yml`. The cost is paid entirely
  by whoever copies the template, which for a template repository is the whole audience.
- **It is three, not four** — wrangler goes with the vestigial worker, per correction 1 above.

[`jekyll-enough`](https://github.com/FCCN-ANTIBODY/jekyll-enough) would close Ruby: a Jekyll build
over an in-memory `path → content` map, no Ruby, nothing installed, four modules importing nothing
but each other.

**It is still not a recommendation to migrate**, but the first pass overstated the obstacle. It said
*"they have `_plugins`"* and left it there. Measured: `_plugins/` is **30 lines in two files**, both
pure Liquid string filters — `clean_title`, `clean_url`, `autolink` — touching no Jekyll internals.
The real Ruby surface is one gem, `jekyll-link-attributes`, and its nokogiri dependency. That is a
smaller wall than we implied, and their call either way; *"your own Jekyll, which is probably already
working"* remains the honest `without:`.

## What we would suggest, in the order it hurts them

### 1. Bottles — because their clock is already running, and their cache cannot be handed to anyone

Their pain, in their code, today. Two distinct problems, and the static framing separates them:

**The gateway.** `bin/pin` is a budget against link death and Pinata is a **gateway** — a
third-party vendor in the read-time path, the one place their own philosophy is violated because
nothing else was available.

**The cache that nobody can hand over.** *Accumulate offline media caches* is realised in OPFS —
the origin-private file system. It works, it is genuinely offline, and it is **per-browser,
per-origin, and unexportable.** A reader who has played a hundred tracks is carrying a hundred
durable copies they cannot give to anybody, cannot back up, and lose with the profile. The most
durable artifact this project produces currently exists only somewhere it can never leave.

**A bottle is the exportable form of that cache** — the artifact carries its own manifest and opens
with a browser and nothing else. No gateway to be up, no pin to keep paid, no CID to resolve through
somebody. Their offline media cache stops being a cache and becomes the artifact.

**And bottles is `draft`.** The vocabulary is settled; the wire format is not. So the honest
recommendation is *not* "adopt bottles":

> **Do not remove Pinata. Do not wait for us.** Keep pinning. And note that the seam we would have
> asked for already exists — `acquireBlob()` takes tiers, cheapest first. What is worth doing today
> is smaller than the first pass claimed: **make the gateway a value rather than a build-time
> template substitution**, so that adding a bottle tier later is an edit to one function instead of
> a rebuild of every page. That is well under an afternoon and it is the whole of the now-decision
> in [`../trade.md`](../trade.md).

### 2. A schedule — because the seat we proposed turned out to be the wrong shape

No listener, no runtime, no service, runnable from a terminal. It wakes, does a bounded amount of
work, writes to its own branch, and opens a pull request. **It is apparatus, in their sense** —
excluded from the artifact, nothing for a reader to depend on.

**Corrected 2026-09-13, and it is the third pass's one finding.** Both earlier passes said
*"`bot/cdn.py` exposes `is_expired()` and `expires_within()`, and nothing calls either in
aggregate."* **That is wrong.** `bot/refresh.py` calls `expires_within` at line 69, walking every
tracked category's `refs.json` — and it does more than count. It re-fetches the originating message
for a fresh signed URL and writes the file back. The repair is written, it is complete, and it is
better than the report we proposed.

What is actually true is narrower and worse:

> **`bin/refresh` exists and nothing schedules it.** `bin/daily` is `init + sync + pin`. Refresh is
> not in it and there is no other caller, so the project can already fix its own link rot and only
> does when a person remembers.

Two things follow, and they point in opposite directions from the original recommendation:

- **A seat that counts is no longer the cheapest real thing.** Proposing a report to somebody who
  has a repair is a downgrade. If a seat is still wanted here it is a different one — *is the
  repair running, and did it keep up* — which is a question about a schedule and not about decay.
- **The cadence is the finding.** Measured from their own committed data, `ex − is` is exactly
  `86400`: every link dies 24 hours after issue. So `bin/daily`'s natural once-a-day rhythm sits
  precisely *on* the link lifetime with no margin, and `refresh` is what buys the margin back.
  Nothing schedules either.

That is a binding problem rather than a code problem, and it is answered by
`residency.yml` in their repository declaring both verbs as `kind: periodic`
([DiscoveryWritten/artist-lockers#1](https://github.com/DiscoveryWritten/artist-lockers/pull/1)) —
written after this fitting, because of it.

### 3. Library — because they already are one and did not know

*A library is already listing what is inside it, because that is what a library is.* `refs.json` is
an enumeration. The site is its rendering. They have the hard half.

Two shapes, and the choice is theirs:

- **Be held.** A library points at their repository; the content stays inert; nobody reads their
  bytes. Costs nothing, reversible, and gets their enumeration into an index others can plug into.
- **Be one.** Mount `.library-engine` and their catalogue becomes federatable — an Atlas plugged into
  it gets the whole index on tap, instead of having to go and crawl for it.

**Their Discord auth is fine, and this is the case that makes the rule concrete.** Our rule is *no
library card* — nothing central may decide whether a change is allowed, and a card may never be a
prerequisite. Theirs is not one, and the library README already blesses it: *a library card is an
establishment's local concern, for their own metrics. Legitimate, and theirs.* Per correction 3,
they satisfy this structurally rather than by policy — the line to hold is not *keep the gate
cosmetic* but **notice that it already is, and that making it otherwise means leaving static
hosting.**

### 4. Tell — because Discord is currently the only door

Everything enters through a Discord message in a category the bot watches. That is a good intake and
it is a **membership** intake: to give them something you must already be in the server.

A Tell is a mailbox for people who hold nothing of theirs. It is inert until spoken to, it needs no
origin anywhere, and it does not oblige them to accept anything — *witness, not judge*; a submission
is never blocked, the submitter learns the outcome instead.

Not urgent. Named because *"there is no way in without a Discord account"* is a decision they should
make on purpose rather than inherit from their bot.

### 5. Atlas — deliberately last, and they have already voted

Routability, once there is something worth pointing at. **Discoverable is not joinable**, and a
publicly discoverable catalogue that admits nobody is a coherent thing.

The static framing turns up a vote we missed: `index.html` carries
`<meta name="robots" content="noindex, nofollow">`. They have explicitly opted out of discovery
already. Atlas is not merely last, it is **contrary to a preference they have stated in the
artifact**, and it should not be raised again until they say the preference has changed.

### What we would not suggest

- **stagecraft** — a render relay. They do not render; nothing to gain.
- **journal** — content-less Jekyll machinery. They have working Jekyll with their own `_plugins`,
  and *"your own Jekyll, which is probably working"* is the honest `without:`. Adopting it would be a
  rewrite in exchange for conventions they have already independently arrived at.
- **civic-node, antidote** — no jurisdiction, and a skeleton respectively.
- **judgement** — they have a media-signal admission rule already, in code they can read. A judge
  ships off and would start as a slower way to do what a regex does. Revisit only if admission
  becomes contested.

## Their decision ledger

| decide now | why now |
| --- | --- |
| delete `worker/`, `bin/deploy-discord-auth`, wrangler | it is dead code with a wrong hardcoded origin in a **template** others copy. Four toolchains become three for free |
| the words: `trade` for the repo, `media` for the holdings | a line in a file today; a migration once anyone federates with them |
| make the gateway hostname a value, not a build-time substitution | they are mid-flight on a pinning layer, and `acquireBlob` is already the right shape. This is the last small thing standing between them and swapping a tier in |
| whether the auth gate is understood to be cosmetic | it is cosmetic by construction. Believing otherwise is the risk, not choosing otherwise |

| decide later | it will still be cheap |
| --- | --- |
| every mount | `git submodule add` in, `git rm` out |
| bottles adoption | the seam already exists; the swap can wait for `draft` to end |
| held vs. being a library | both reversible, and doing one first does not spend the other |
| a Tell, more seats | independently adoptable, in any order, none obliging the next |
| an Atlas | not on the table while `noindex` is in the artifact |
| running anything at all | a mounted engine starts nothing. **The claim is a menu, not a startup script** |

## What this fitting taught us

The point of publishing the fitting rather than the conclusion. The first pass's six findings stand;
the second pass added three, and the first of them is about the first pass.

1. **They needed a door before they needed a repository.** Nothing in this project would have led
   anyone to `bottles.anecdote.channel` — you would have to already know a bottle was the answer to
   find the document that gives it. This is the argument for a centralized entry point stated as
   evidence instead of as an opinion. [`../../ADOPTING.md`](../../ADOPTING.md) exists because of it.

2. **The wedge was found by reading their code, not by them reporting it.** Nobody was withholding
   anything; from inside their project nothing is wrong, because a custody layer *is* the right thing
   to build when there is no other. Our only current discovery mechanism is *somebody reads your
   repository*, and that scales to roughly one adopter. Named in [`../trade.md`](../trade.md); no
   mechanism proposed, because we do not have one.

3. **Ranking by pain inverted our architecture, and the inversion is right.** Read bottom-up —
   origin, engines, categories — bottles is deep infrastructure. Read from their problem, it is the
   first thing and everything else can wait years. Every door in [`../`](../) should rank by pain,
   and the roster ordering in `ADOPTING.md` is for orientation only.

4. **Ranking by pain points at our least-finished work, and it will keep doing that.** Their
   top-ranked engine is `draft`. That is not a scheduling accident: the gaps that hurt adopters most
   are the gaps we have not closed. So an onboarding document has to be able to say *this is the
   right answer and it is not ready*, and to give a useful now-move anyway.

5. **The fitting missed a whole family on the first pass.** `-enough` was not in the roster at all,
   so the alignment that mattered most to a *no frameworks* project was the one the primer could not
   surface. Fixed in [`../../ADOPTING.md`](../../ADOPTING.md); the general lesson is that **a
   convention is a thing to onboard people into, exactly like an engine.**

6. **One project holds more than one category's worth of obligation, and cannot say so.** `trade`
   repo, `media` holdings, `voices`-shaped consent duties toward the artists in it.
   [`../../OPEN.md` §10](../../OPEN.md).

7. **A fitting written from the README describes a project that does not exist.** Every one of the
   three corrections above came from reading code the README summarises accurately but incompletely:
   the worker is documented under *Tooling* and is dead; the addressing seam is undocumented and
   built; the auth is described as gating and decorates. **The first pass recommended two things they
   had already done and credited them with one thing they had not.** A fitting has to read the
   artifact, not the description of it, and this one now says which file and which line for every
   claim it makes.

   **And that promise was not enough, which is the third pass's lesson.** The sentence above was
   written in the same document that claimed *"nothing calls either in aggregate"* — a claim about
   `bot/refresh.py`, which does. Citing a file and a line disciplines a **positive** claim and does
   nothing for a **negative** one: *this exists, here* is checked by reading one place, while
   *nothing does this* is only ever checked by searching every place, and neither pass ran the
   search. Two passes asserted it and both were confident. **A negative claim is a grep you have not
   run yet**, and in a fitting it is also the most dangerous kind, because every "they have not built
   X" is a recommendation to build X.

8. **We assumed a server, because our own vocabulary has one.** Engines, seats, relays and mailboxes
   all presume something that can be running. This project's answer to nearly every question is *it
   is a file that was already built*, and the first pass kept reaching past that — attributing auth
   to a worker rather than to PKCE in the page, proposing a seam rather than finding one in
   `player.js`. **Static is not a deployment choice here, it is the design**, and a fitting for a
   static project should start by sorting the repository into apparatus and artifact, which is what
   this pass did and what turned up all three errors.

9. **Their `exclude:` list was a better statement of our own principle than ours was.** We say
   *everything must stay runnable by hand* and *the host must not become a dependency*. They say it
   as a config block that names, exhaustively, what the published thing does not contain. **A
   project can hold a principle in a form we do not recognise as a statement of it**, and the only
   way to find that out is to read the configuration and not just the prose.
