# README is the index

`status: draft` — written 2026-09-13. **This document decides what a library serves when somebody
lands on its bare address, and it decides it aggressively.**

The answer is `README.md`. Not `index.html`, not a landing page, not an index with a README button
in the corner. **The first thing you see is the README**, and everything else is reached from it.

## The two postures, and why the softer one was refused

There is a graceful version of this and it was on the table:

> Serve the index. Put a **README** button next to it, always visible, for anyone who wants the
> real document.

It is reasonable, and it loses. Three reasons, in increasing order of how much they matter:

1. **A button is a thing you have to notice.** The person who most needs the README — a stranger,
   arriving cold, with no idea what this project is — is exactly the person who will not go looking
   for an alternate view of a page that already looks finished.
2. **An index is where a project puts what it wants you to think.** A README is where a project
   puts what you need to know. Those drift apart, always, and the index wins every time it is the
   default, because it is the one anybody bothers to keep pretty.
3. **It is a way to completely sidestep a poisoned index.** An index page is the artifact the old
   web optimised: it carries the tracking, the consent wall, the interstitial, the thing that was
   built for a visitor rather than for a reader. Making README the door is not a stylistic
   preference. **It is a toggle out of a surface that has been captured**, and offering it as an
   option rather than as the default concedes the thing worth taking.

So the posture is the strong one. If a project wants a designed landing page, it links to one,
iframes one, or exhibits one — from the README. The README stays the door.

## Why capitals

The canonical files in this constellation are **uppercase**: `README`, `CONSTITUTION`, `AGENTS`,
`OPEN`, `NAME`, `LICENSE`. That is not shouting and it is not legacy. **The capitals are the
namespace.** They mark a small, fixed, cross-repository set of top-level concerns, each of which
means the same thing in every repository that has one — which is precisely why they can be rendered
as buttons by something that has never seen this project before.

`INDEX.md` would be acceptable. **`index.md` would not**, and the difference is the whole scheme:
lowercase is a project's own vocabulary, and a renderer may not assume anything about it.

### The canon, and what each one promises

| file | promises |
| --- | --- |
| `README` | **the door.** What this is, and where to go next. Required |
| `NAME` | the one-line identity, machine-first |
| `CONSTITUTION` | what this service is bound by, in plain words, before it is coded |
| `AGENTS` | how to work *inside* this repository |
| `LICENSE` | the terms — and for a library, **the terms attached to what it has custody of**, which is not the same document as the terms on its code |
| `OPEN` | what is deferred and unsolved here |

A repository is not obliged to have any of them but `README`. **A canonical name may not be
repurposed** — the same refusal [`CATEGORIES.md`](CATEGORIES.md) makes about reserved words, and
for the same reason: a renderer that cannot trust the name has to be told, and being told does not
scale past the first repository.

## The metatags are the front matter

A canonical file is declared in the README's **front matter**, and that is the whole mechanism:

```yaml
---
permalink: /
constitution: CONSTITUTION.md
license: LICENSE.md
agents: AGENTS.md
---
```

Two things fall out of this, and both are why it is front matter rather than a separate manifest:

- **A renderer that knows the scheme draws buttons.** It reads the keys it recognises, ignores the
  rest, and needs no configuration from the project.
- **GitHub renders front matter as a table at the top of the file.** So a reader with no renderer
  at all still sees the canonical files, in a list, before the prose. **That is not a degradation
  artifact to apologise for — it is the metatags, displayed.** It was the deciding argument for
  front matter over a sidecar file.

`permalink: /` is what makes the README build to `index.html`. See "how it builds", below.

## The strip

**The first link list after the title is the navigation.** Not a tag, not a component — real
markdown links, in a list, in the position where a reader would look for them anyway.

```markdown
# library.anecdote.channel

[Adopting](ADOPTING.md) · [Categories](CATEGORIES.md) · [Residency](RESIDENCY.md) · [Open](OPEN.md)
```

On GitHub that is a row of working links. In a renderer that knows the scheme it is a **tab strip**,
and the panes open underneath it — the same documents, iframed, without leaving the page.

**The upgrade path is the point.** Nothing has to be added to the markdown to make the strip work,
and nothing breaks when the renderer is absent, because the fallback *is* the source: a list of
links to documents that exist. A component that degrades to a list of links is strictly worse than
a list of links that upgrades to a component.

## The degradation contract

Three renderings of one file, and the rule that binds them:

| rendering | who sees it | what they get |
| --- | --- | --- |
| **source** | anyone with the raw file | the markdown, as written. Tags visible, and legible |
| **GitHub** | anyone with the repository | markdown → HTML, front matter as a table, links as links. **The screen-reader version** |
| **exhibited** | a renderer that knows the scheme | the strip as tabs, panes as iframes, canonical files as buttons |

> **The rule: a tag's parameters must read as prose.**

This is what makes the source rendering *legible* rather than merely *present*. When a reader with
no renderer meets an embed, they do not see a broken component — they see a sentence explaining
what would have been there and why.

The idiom already exists and is not being invented here. From the journal engine's `iframe.html`,
as used in the citation journals:

```liquid
{% include iframe.html file="tns.pdf"
  side="left"
  overview="Official PDF for the movement."
  caption="This document is greatly detailed and you should use AI or any means to understand
           what is inside this file directly, not just what AI synthesizes from the sources."
%}
```

`overview` is the accessibility string — it becomes the iframe's `title` — and it is **deliberately
not called `alt`**. A parameter with a boring, familiar name gets filled in boringly, or skipped.
`overview` asks a different question and gets a different answer, and the answer is the sentence a
source reader actually needs.

**When we say iframe, we never mean a free-range iframe.** An embed arrives through an include, the
include is a named, reviewed template, and the tag's presence in the source is the signal that
something richer is available here. That signal is the feature: seeing an include is how a source
reader knows they are looking at the reduced version, and that a fuller one exists.

## What a library exhibits

A library's README is its **home exhibit** — the guided way in, chosen by whoever runs it. The word
is already in use for a sibling thing (`civic-node`'s `bin/exhibit` builds a guided chronological
reading of a channel) and the sense carries: **an exhibit is a curated reading, not a dump.**

That makes the README a genuinely different document from what a README usually is. Most of them
are half dev-setup and half whatever the last person needed, and almost none of it is relevant to
a visitor. The demand this scheme makes is the useful one:

> **If it is not reachable from the README, it is hard to see.** Put the way in there, or accept
> that nobody finds it.

You are free to link to pages that do more. You are free to exhibit pages that do more. What you
may not do is have no door.

## How it builds

[`jekyll-enough`](https://github.com/FCCN-ANTIBODY/jekyll-enough) does it, in a tab, with nothing
installed — `buildSite` takes a `path → content` map and returns one, never touching a filesystem.

The mechanism is small enough to state completely:

1. A file is a **page** if it has a front-matter fence. Without one it is copied verbatim.
2. `permalink: /` sends a page to `index.html`.
3. So **`README.md` with front matter *is* `index.html`.** There is no second file, no redirect,
   and no generated stub.

That last point is the one worth guarding. **The URL does not move.** A visitor landing on the bare
address is not bounced to `/README`, does not watch the location bar change, and never gets the
feeling of having been sent somewhere that might be a dead end. They asked for the library and the
library answered — with its README, because that is what the library's front page *is*.

For a host that insists on a literal `index.html` in the tree, the same build produces exactly
that. The bridge and the document are one artifact.

### Measured, and the one thing it exposes

Run over this repository as it stands: 19 files in, **`README.md` → `_site/index.html`**, front
matter consumed rather than printed, the strip emitted as four working anchors. One page rendered
and everything else copied verbatim, because only the README carries a fence.

That last part is the honest edge. **The strip's links point at `.md` files**, and a plain static
host hands a browser raw markdown when somebody clicks one. It is right for the two renderings that
matter — GitHub renders linked markdown, and a scheme-aware browser renders it itself — and it is
wrong for a dumb file server.

The wrong fix is to fence every document so it builds to HTML: the links would then have to name
`.html` targets that do not exist in the source, and the source is the thing a reader without a
renderer is holding. **The source links stay source links.** A renderer resolves them; a file
server does not, and that is a property of the file server.

## What is not decided here

- **The renderer.** This document specifies what a source file promises. Which renderer draws the
  strip as tabs, and how, belongs to `anecdote.channel` — the browser is the consumer and the
  scheme is deliberately implementable more than once.
- **The button set beyond the canon.** `LICENSE` for a library plausibly means *the terms on what
  it holds*, which is a different document from the terms on its code and may need a different
  name. Named, not answered.
- **What a library branch exhibits when it cannot serve HTML at all.** A library backed by IPFS may
  have an index and no README to serve; the content is in the bottle, and opening the bottle is
  what produces the exhibit. Recorded in [`OPEN.md` §11](OPEN.md).
