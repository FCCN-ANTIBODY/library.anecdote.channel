# The reserved words

`status: draft` — written 2026-09-11. **This repository reserves; it does not canonize.**

A category is **a tag that got promoted**. `voices`, `media`, `trade`, `city`, `bottles`,
`library` are the same kind of thing as any other tag — the difference is only that they occupy a
level of a hostname and render as a directory. Picking a super-category is picking a tag and
saying *this one is a place*. That is worked out in
[`civic-node/docs/proto-issues/super-categories-are-derived.md`](https://github.com/FCCN-ANTIBODY/civic-node/blob/main/docs/proto-issues/super-categories-are-derived.md),
and it is not restated here.

## Reserving is a different act from deriving, and they do not conflict

They answer different questions, which is the whole reason both can be true at once:

| | the question | who answers |
|---|---|---|
| **derivation** | *what is this thing?* | the Atlas, from labels the reducer crunched. **Nobody sends a "trade anecdote."** |
| **reservation** | *what does this folder mean?* | **the library, in advance, about a word at its top level** |

A library rearranging itself may do almost anything — moving is a `.gitmodules` edit and a
`git mv`, and rearranging is expected rather than exceptional. **What it may not do is repurpose a
reserved word.** `trade/` is the trade category or it is absent. It is never a vendor folder that
happens to be called that.

## The words

| word | what it means | status |
|---|---|---|
| `voices` | people writing | reserved |
| `media` | broadcast | reserved |
| `trade` | business, money or not | reserved |
| `city` | the civic node, and what a jurisdiction publishes about itself | reserved |
| `bottles` | the crate you send something in | reserved |
| `library` | knowledge | reserved |
| `land` | shapes, and who claims them | **proposed 2026-09-11 — not canon.** See below. |

**`library` inside a library is legitimate and not a mistake.** Two buildings across a city both
listing a book is redundancy rather than conflict, and the same holds one level up: a library
holding another library's catalogue is the useful fact that the thing is available in more than
one place. Being forced to be one *category* is what makes the word canonical; being forced to be
one *collection* would not.

## Spoken for, and not categories

Two more words are taken at a library's top level, and **neither is a category.** They are
**shelves** — a library's own working prefixes — declared in [`SHELVES.md`](SHELVES.md):

| word | what it means | status |
|---|---|---|
| `share` | held in order to be handed on. Where moniker groups belong | reserved, **not a category** |
| `build` | intermediates the library made and sources deterministically | reserved, **not a category** |

They are registered here for one reason and it is the reason this file exists at all: **they are
bare words at the top level, so they can collide with a future category, and un-reserving is
expensive.** A library whose `share/` held the trade category, or whose `build/` was promoted to a
category word by somebody who did not know, is the exact federation failure the rest of this
document is written to prevent — an Atlas plugged into two libraries getting two meanings for one
word, with no repair that is not a migration of somebody's tree.

Wings did not need this. A wing always begins with `.` and a category never does, so they cannot
collide by construction. **Shelves are bare words and can**, which is why they get a line here
rather than only a document of their own.

The three refusals in the next section apply to these two as well, with one substitution: a shelf
may not be promoted *to* a category, and a category may not be demoted to a shelf.

## Why forcefully, and why now

**Reserving costs nothing and un-reserving is expensive.** Introducing `library` cost nothing
structurally — unserved levels already render as categories — and that asymmetry is the entire
argument. A word held in reserve is a line in a file. A word taken back is a migration.

**The cost of not reserving is paid by somebody else.** A library whose `trade/` holds something
that is not the trade category cannot be federated: an Atlas plugged into two libraries gets two
meanings for one word, with nothing to say which is right and no repair that is not a migration
of somebody's tree. The failure does not surface where it was caused.

So *forcefully* means three refusals, and they are for a caretaker to obey:

- **A category folder may not be renamed away** by a round that is tidying.
- **A reserved word may not hold non-category material**, however convenient.
- **A seventh word may not be taken locally.** Proposing one is welcome and cheap; *taking* one
  is the thing that cannot be undone from here.

## What reservation does not do

- **It does not require the folder to exist.** A library reserving `media` and `city` with
  nothing in them is correct — empty groups teach a reader nothing, and reserving a word costs
  no directory.
- **It does not make the library the authority on what is *in* the category.** That is derived,
  from labels, by something else, and an author does not declare it.
- **It does not promote a word to a super-category constellation-wide.** *What promotes a tag* is
  genuinely open — frequency, an operator's declaration, the existence of a node already serving
  at that hostname level — and today the answer is *somebody said so*, which works for six words
  and will not work for sixty. That question belongs to `anecdote.channel`.

**The distinction to hold onto:** this repository writes down which words are spoken for, and
what a library owes each one. Whether a word *becomes* a category is decided elsewhere.

## `land` — proposed, with the reasoning it was proposed with

Raised by the operator 2026-09-11. Recorded as proposed rather than adopted, because the
promotion is not this repository's to make — but the reservation is cheap and the reasoning
should not be re-derived later.

**The artifacts are geoJSON, and the library would be the viewer.** Nodes already want to talk
about shapes; there is nowhere that holds them.

**Competing definitions are the normal case, not a defect.** There are standing border
disagreements, and they exist because people disagree rather than because a design invited them.
So the posture is the one the library already has everywhere else: **hold both, enshrine
neither.** A library that reconciled two boundary claims would be adjudicating, which is the
thing it does not do.

**And land has a property the other six do not.** Some of it is under your feet, and some of it
you go and fight for. People care about land beyond their own borders, and not idly: it might be
a river, a road, where a trade partner sits, or the shape of a place that catches fire a lot. A
node stockpiling shapes it does not administer is therefore **the ordinary case, not the
exception** — and any design that assumes a jurisdiction only holds its own outline has already
got it wrong.

Local use is the other half and it is smaller-grained than a border: community farming, what a
strip of ordinary residential parkland could be used for. The shapes are the same kind of object.

**One thing to check before this is adopted.** [`OPEN.md` §8](OPEN.md) asks whether a library may
be **constituency-bounded by geoJSON**. If `land` is a category, then the thing that bounds a
library is also a thing a library holds. That is either elegant or circular and **nobody has
looked.** It is the first question `land` should have to survive.

## `city` holds document *structure*, not only documents

The concrete thing the city word is for, and it is easy to under-read.

A city can publish everything openly and still be a needle-in-a-stack problem — Fort Collins is
the worked example, where the documents are genuinely all there and finding one is still hard.
Two failures, and the second is the interesting one:

1. **Finding it at all.**
2. **Keeping a live link to a *rolling* document.** *"The last council agenda"* and *"the coming
   council agenda"* are descriptors whose target moves. A link to one goes stale **by design**,
   not by neglect, and no amount of care on the linker's part fixes it.

So the artifact a `city` section holds is often **not the document**. It is what is known about
the document's *shape*: where in it a given thing lives, how to walk it, and how a rolling
descriptor resolves this week.

**This is explicitly not OCR.** The claim is *"we have studied this document because we
understand its format, and here is how you crawl it"* — a **crawl recipe**, which is a claim about
structure and is therefore testable against the next issue. Extracting text from a picture is a
different and weaker thing.

It is also why `city` decays on a real clock: **a city changes its publishing system without
telling anyone**, and a recipe that used to work stops silently. That is a health property no
other category has in the same form, which is the next section.

## Health is a function of what the thing *is*

The reason a single "is the library healthy" seat is the wrong shape. Preserving images and
preserving repositories are not the same job, and a seat told to do both well has been told to do
two jobs.

| category | what "healthy" means here | how it fails |
|---|---|---|
| `voices` | attribution is intact and the writer can still withdraw; superseded pieces are visibly superseded | a piece outlives its author's consent, or a byline points nowhere |
| `media` | the artifact still **plays** | bytes preserved perfectly in a container nothing decodes any more |
| `trade` | a nameplate still resolves to a live party; a template still builds; nobody is wedged into a workaround by a gap in *our* tools | everything is present and nothing works; the gap is invisible from inside any one holding |
| `city` | the crawl recipes still find what they name, and rolling descriptors still resolve | the city changed its publishing system and nothing said so |
| `bottles` | custody still checks, and a bottle still opens for a tool handed one file and nothing else | playback acquires a build step; a construction is mistaken for a clean seal |
| `library` | the enumeration is honest — what it says it has, it has | the catalogue drifts from the stacks; this is the clerk's ground |
| `land` *(proposed)* | the geometry parses, the provenance of a shape is recorded, competing claims sit side by side | two claims silently reconciled into one, and nobody can tell which was kept |

Each row is a different seat's job. [`SEATS.md`](SEATS.md) is what that means in practice.
