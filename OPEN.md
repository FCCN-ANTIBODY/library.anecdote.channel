# Open questions

`status: draft` — written 2026-09-03 while stubbing this repo. None of these is decided.

> **Narrowed 2026-09-03.** §1 and §2 below turned out to be one question wearing two hats:
> **how does a Tell server with a library talk about the content on it?** Everything is isolated
> today; the open part is what it means for it *not* to be. The sharpening is in §2.

## 1. Does `library` subsume `bottles` as a subdomain concept?

**The observation that raises it:** every mechanic of checking a bottle out, writing to it, and
putting it back is **identical** whether the bottle sits under a `bottles` subdomain or a `library`
one. Who owns it and who may modify it are not special-cased anywhere. If the mechanics are the same,
two subdomain concepts may be one concept with two names.

**What argues against collapsing them.** A library is **not the same kind of diverse node** another
category is. `bottles.<apex>` is D4/D11's free-form cubby space — arbitrary origins, storage engines,
anything. A library is a curated, enumerating collection with an admission posture. Those are
different jobs even when the lending machinery is shared.

**What argues for it.** Having both a bottles engine and a library engine installed on one node —
say a Tell server — looks like two tools doing one job. A single tool would be a clearer path.

**Not resolvable from here.** It touches D4 (bottles topology) and D11 (storefront and intake), so it
is a constellation decision, not this repo's to take.

## 2. A library installed on someone else's node — what makes it discoverable?

A Tell server can run a library. But **a Tell registering with an Atlas means the Tell was
discovered — not that every tool on it is public.** Registration discovers the node, not its
contents.

### The candidate answer: the Atlas is the UI

If a Tell registers, you know the repository where its library is kept. If that library's contents
are public, **the Atlas can enumerate them**, the same way it already categorises polls and
everything else. Which produces a genuinely simplifying possibility:

> **The library may not need a bespoke UI at all.** The Atlas is the directory. A library on a Tell
> probably still *has* one — it is a side system with its own surface — but it should not have to.

That is the strongest argument yet that a library is a kind and not an application: its whole job is
enumeration, and something upstream already enumerates.

### The constraint that stops it being automatic

**A Tell may hold a private pile of library knowledge.** Not encrypted — just *theirs*. They have it
here, and registering the Tell with an Atlas must not hand it over. So discovery cannot be a
side-effect of registration; **it has to be an act.**

Which is the same shape as the public-project-restricted-contribution case: a public item that not
everyone may write to, because writing is governed by the hooks and not by the library. Read and
write are already separate here; **public and discoverable have to be separated the same way.**

### The new relationship: a library registers to a Tell

A council registering its findings into a library is not the same act as sending an anecdote, so a
registration flow is in the cards — and the words that go with it are **a library registers to a
Tell**. That phrase has not existed before, and it has been a long time since anything new registered
to anything, so it deserves to be designed rather than assumed by analogy.

Open inside it: what a library's registration *grants* (enumeration? ingest? both, separately?), and
whether de-registration leaves the Atlas holding a stale index.

## 4. The Tell is the authentication control point — probably

Separate from discovery, and possibly the more load-bearing of the two.

**Discoverability and reachability are not the same thing.** A Tell server is not public or
discoverable, and that says nothing about whether the people inside it can talk to it. They can. What
is missing is where they *authenticate*.

The instinct, and it is a good one: **if a Tell is exposed at all, the Tell is the control point, for
the whole Tell.** One passkey, usable across the services running on it. The alternative — the
library authenticating separately from every other tool on the same node — means a member who signed
up for a Tell does not feel signed up for the things on it, which is close to the opposite of the
point.

To be explicit about what this is *not*: **no device accounts are auto-created for anybody.** Nobody
is enrolled by being nearby. The claim is only that when a person does make a passkey, one is enough.

**The collision to resolve before building it.** A passkey is scoped to an RP ID, and D12 already
ruled *one RP ID, at the `you` keeper*. "The Tell is the control point" and "one RP ID at `you`" are
either the same statement seen from two ends — the Tell is where you *use* it, `you` is where it
lives — or they are in conflict. **Nobody has checked which.** That check is the next real piece of
work here, and it belongs in `anecdote.channel/docs/decisions.md`, not in this repo.

Related and unsolved: exposing a public data pile at all (journal exhibits, for instance) needs both
passkey authentication and a name on the DNS system. The Tell is the only thing in the picture that
plausibly has both.

## 3. Where does the `you` engine belong — the library, or the node running it?

*(§4 below is the same question from the other direction, and leans the same way.)*

Stated both ways in the same breath, and **the node is the better instinct.** A library does not
authenticate anybody (see the no-library-card section in the README); the thing a person authorizes
*against* is the node they are standing on. Mounting `.you-engine` here would imply an identity
relationship the design explicitly does not want.

The counter-case: if a library ever wants a voucher on a stable identity — not to gate reading, but
because it wants to know that the same masked person came back — the passkey a person already carries
is what it would want, and it has to reach it somehow.

**Leaning: the node mounts `.you-engine`; the library never does.** Not settled.

### Sharpened: it is not required, *unless* it is how a grant is understood

Walking it through settles most of it. A person does not need the `you` engine to **get into** a
Tell. They might need it to **look at things on the Tell that are managed outside it** — and library
content is exactly that, because **library content never gets written into the Tell.** It is not
clear what that would even mean.

The one thing it plausibly means is **notification**: the Tell tells you when something entered the
library. That is a natural fit — delivery is already a Tell's job — and it may turn out to be part of
what registering a library to a Tell *grants* (see §2). It requires no identity engine.

So: **the `you` engine is not required — unless it is the way a grant to take something out of the
library is understood.** That is the whole hinge, and it is now the only version of this question
worth asking.

## 5. The library keeps its bottles in data-piles, and that is a custody proof

Not an identity question, but it is what §3's hinge turns on.

**Assume everything the library holds travels as a bottle**, because that is how everything travels
now. It does not strictly have to: a library may keep files that need no bottle and **package one in
a clean bottle to send it** — D17's canonical empty bottle, doing exactly the job it was named for.
The bottle stays the target either way.

Now put those bottles in **data-piles**, and three things fall out:

1. **When a thing entered the ecosystem** is legible from the git log, without anyone maintaining a
   separate accession record.
2. **You cannot write to the bottle without getting it out of the pile** — which is the outer of the
   two hook layers (`civic-node` `OPEN-QUESTIONS.md` §AA), arriving here as a practical consequence
   rather than as a rule someone imposed.
3. **The pile is a stewardship proof.** This is the new part and the sharp one.

### Custody, not existence

A signed bottle proves **the thing exists and this is its version**. A library holding that bottle in
a pile proves something strictly more: **that this library has it, and has had it since then.** Those
are different claims and only the second one is what a library is *for*.

The mechanism is ordinary — run the thing through the machine that puts it in a pile, and it is
logged there permanently and can be revealed repeatedly. What it buys is not novel cryptography; it
is that custody becomes a fact somebody can check.

### And explicitly not a redaction service

**A library should not be doing redaction footwork.** Its job is not to reveal-with-redaction; you
may already have the full documents, and it is not the library's business to be the one deciding what
of them you see. Piles support redaction because piles support it for their own owners — that
capability is theirs, not a service the library offers on others' behalf. If library work starts
requiring redaction judgement, that is a signal something has been put in the wrong place.

## Related, elsewhere

- **The control QR.** The `discoverywritten` work wants it for onboarding onto the bottle surface.
  The thought worth carrying: **it is more powerful if what you receive is a *library item* — which
  is a bottle — than a bare bottle.** An item arrives with provenance, a place it came from and
  something that enumerates it; a bare bottle arrives with none of that.
- **The signers-list amendment request** — the one message a borrower may need to send. No shape yet;
  must stay optional and stay small.
- `civic-node` `OPEN-QUESTIONS.md` §AA — the two layers of hooks, and loaning as a grant of write.
