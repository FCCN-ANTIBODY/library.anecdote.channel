# One door per word

`status: draft` — written 2026-09-13. The general door is [`../ADOPTING.md`](../ADOPTING.md); this
directory is where it sends you once you know which word you are.

## Why a door per category, and not one big onboarding

Because **health is a function of what the thing is.** [`../CATEGORIES.md`](../CATEGORIES.md)
already says this about seats: preserving images and preserving repositories are not the same job,
and a seat told to do both well has been told to do two jobs. Onboarding inherits it exactly.

What a `media` adopter needs to be told first is *the artifact has to still play in ten years*.
What a `city` adopter needs to be told first is *your crawl recipe will break silently when the
city changes its publishing system and nobody tells you*. What a `trade` adopter needs to be told
first is *if our tools have a gap, you will paper over it and we will never find out*. Those are
not three emphases of one document. They are three documents.

**A word without a door is not a defect.** Reserving costs nothing and un-reserving is expensive,
so the words were reserved ahead of the writing on purpose. An empty row below means nobody has
needed that door yet.

## The doors

| word | door | status |
| --- | --- | --- |
| `trade` | [`trade.md`](trade.md) | draft — the first one written |
| `voices` | — | owed |
| `media` | — | owed |
| `city` | — | owed |
| `bottles` | — | owed. Note the exception: somebody who meets a bottle in the wild **onboards with the bottle**, and should never have to find us first |
| `library` | — | owed |
| `land` | — | not until the word is adopted; it is *proposed*, not canon |

## The fittings

A door gets written by fitting a real project and publishing what the fitting exposed.

- [`worked/artist-lockers.md`](worked/artist-lockers.md) — the first. A Discord-sourced media
  catalogue that had already built its own custody layer because ours did not exist.

**Publish the fitting, not just the conclusion.** The conclusion ages into a recommendation nobody
can argue with; the fitting keeps the reasoning next to the project it was reasoned about, which
is the only form a later adopter can check against their own situation.

**And then let it go when it has been paid for.** A fitting is about a real project at a real
commit, and once that project has onboarded, keeping a public reading of it is a courtesy nobody
asked for. Retiring one is expected: the method above is what the fitting was *for*, and it stays.

## How to run a fitting, and why the file is disposable

**A fitting is a method, and the method is the durable part.** The write-up is a reading of one
project at one commit; it ages, it belongs to somebody who may finish onboarding and move on, and
**deleting it should cost nothing.** It costs nothing because everything transferable is here.

Nine rules, all of them paid for by getting something wrong first.

### Read the artifact, never the description of it

**A fitting written from the README describes a project that does not exist.** Not because a README
lies — because it summarises accurately and incompletely, and the gaps are exactly where the
interesting facts are. The first fitting's first pass recommended two things the project had already
done and credited it with one thing it had not.

So: **name the file and the line for every claim.** A fitting that cannot cite is guessing.

### Sort the repository into apparatus and artifact before anything else

**We assume a server, because our own vocabulary has one.** Engines, seats, relays, mailboxes — all
of them presume something that can be running. A great many projects answer nearly every question
with *it is a file that was already built*, and a fitting that keeps reaching past that will
attribute behaviour to machinery that is dead code.

Static is not a deployment choice for those projects; **it is the design.** Sorting the tree into
*what runs* and *what ships* is the cheapest step and it surfaces the most errors.

### Read the configuration, not just the prose

**A project can hold one of our principles in a form we do not recognise as a statement of it.** We
say *everything must stay runnable by hand* and *the host must not become a dependency*; the first
fitting's project said the same thing better, as an `exclude:` block naming exhaustively what the
published artifact does not contain.

Look at the config files. They are where a project states its principles operationally, and
operational statements are stronger than the ones in the README.

### Rank by pain, not by our architecture

Read bottom-up, our infrastructure has an order. Read from an adopter's problem, that order inverts
— and **the inverted one is right.** Every door here ranks by what hurts; the roster in
[`../ADOPTING.md`](../ADOPTING.md) is for orientation only.

### Expect the ranking to point at our least-finished work

It is not a scheduling accident: **the gaps that hurt adopters most are the gaps we have not
closed.** So a fitting must be able to say *this is the right answer and it is not ready* — and
still hand over a useful move for today. A recommendation to wait is not a recommendation.

### The wedge will not be reported to you

From inside a project that worked around a gap in our tools, nothing is wrong; building the missing
piece *was* the right call. So the discovery mechanism is **somebody reads your repository**, which
scales to roughly one adopter, and that is a weakness in our design rather than a duty of theirs.
Say so in the write-up. See [`trade.md`](trade.md), "the wedge".

### A convention is a thing to onboard people into, exactly like an engine

The first fitting missed the `-enough` family entirely, so the alignment that mattered most to a
*no frameworks* project was the one the primer could not surface. **A naming scheme that has to be
noticed rather than read is doing half its job.**

### Do not tell an adopter their word is ours

Where a project already uses one of our words in its ordinary sense — and it usually predates us —
**the convergence is a point in the word's favour, not something they reconcile to.** *Our term of
art, which you now also use* is both wrong and the thing that makes onboarding feel like
assimilation.

### Expect one project to owe more than one category

`trade` repository, `media` holdings, `voices`-shaped duties to the people inside it. There is
nowhere to write that down yet — [`../OPEN.md` §10](../OPEN.md) — so record which obligations you
found rather than forcing a single word.

## What a door owes

Each one should answer these five, in this order, because it is the order they bite:

1. **What does this word mean here**, in one paragraph, without restating `CATEGORIES.md`.
2. **What does healthy look like, and how does it fail** — the row from the health table, expanded
   into something an adopter can recognise in their own repository.
3. **What could you use today**, ranked by *your* pain and not by our architecture.
4. **What must be decided now, and what may be decided later.** An adopter is entitled to know
   which doors close behind them. Almost none of ours do; say which.
5. **What we do not have yet**, plainly. A gap named is a petition somebody can file. A gap
   unnamed is a workaround somebody builds alone, and we never find out.
