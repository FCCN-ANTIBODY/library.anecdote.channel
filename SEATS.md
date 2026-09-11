# Category seats — what it means to own a category

`status: draft` — written 2026-09-11. Companion to [`CATEGORIES.md`](CATEGORIES.md), which says
which words are reserved and what each one's health means.

## The problem, which is not a capacity problem

The instinct is that one *"keep the library healthy"* seat gets overloaded as the library grows,
and that the fix is a bigger budget or a better model. **It is not.** The fix is that
**health is not one question.** A seat told to keep repositories, images, crawl recipes and
boundary shapes healthy has been handed four jobs and one voice to say them in — and the first
thing it will do is flatten them into whichever one it understands best.

Splitting by category splits along the seam that is actually there. That is what makes it a
different thing from sharding work across more agents.

## What a category seat is

**One seat, attending one category of one library.**

- **Its mission comes from the category**, and the category is this engine's —
  `CATEGORIES.md`'s health row is the mission, already written, not guessed per library.
- **Its constituency comes from the people who stocked it**, and that is the operator's. Two
  libraries holding `trade` have the same health definition and different constituencies, which
  is exactly the right place for the difference to live.

**The engine ships the word; the instance seats it.** Nobody's library needs the same seats as
anybody else's — a library with nothing in `media` should not have a media seat, and no config
here should imply otherwise. See [Where seats are declared](#where-seats-are-declared).

## Ownership is not advocacy for the contents

The obvious misreading, named so it does not happen: **a trade seat does not promote the projects
in `trade/`.** It is not a marketing function and the holdings are not its clients.

What it does is closer to **reconnaissance**. The shape, in the operator's framing: a seat
notices that several holdings *"are forced into a pattern of doing this thing because our tool
doesn't really do that"* — because the engines underneath them do not support something. Each
holding worked around it alone and could not see that the others did too.

Two properties make that worth a seat rather than a survey:

- **The finding is about the tool, not about them.** It graduates into a petition aimed upstream,
  once, on behalf of a pattern — not a note filed against each holding.
- **It is only visible from where the seat sits.** No single holding can see it, and nobody who
  can see it has a reason to look. That is the definition of a caretaking concern.

## Reading across holdings is a grant, not a default

**The tension, stated plainly rather than finessed.** A library's caretaking rule is that held
content is **inert** — not read, not consulted, not used to judge, with the *reading* refused and
not merely the obeying. Reconnaissance reads. Those cannot both be unconditional.

**Admission is where it resolves.** Stocking a library is self-service and opt-in, so a stocker
opting into reconnaissance is **a term of admission, carried per item.** Absent that term, the
content stays inert and the seat works from what is visible from outside — names, dates, sizes,
what a submodule points at.

Three things that survive intact, which is why this is the right resolution and not a carve-out:

- **No front desk.** The library is not adjudicating anything. It is honouring a term that
  arrived *with* the item, which is the same posture as everything else here.
- **A public library's version is legitimate**, because people registering a project opt in
  visibly and can decline. They *"handshake their way into participating."*
- **The default stays the strict one.** A seat that was handed nothing reads nothing.

**Not designed yet, and it should not be improvised: where the term is written.** The bottle's
own manifest is the obvious candidate and would mean the grant travels with the item rather than
living in a table the library has to keep. Until that exists, a category seat reads only what it
was explicitly handed.

## Budget, and the cursor

The same shape the library's own tending already uses, because the same thing is true of it: the
concern is **designed to sprawl**, so it is spent rather than swept.

    budget: N        units tended per round, spent from the top down
    cursor:          where the last round stopped

**Deferral is close to free, and that is load-bearing.** What a category needs done is
cumulative: a group tended three rounds late gets the same work, slightly larger. Nothing
expires, so a cursor is enough and a priority queue is not needed.

**The cursor advances only on a completed write.** A round that crashed did not move it, so its
slice is served again next time. That is the entire recovery story and it is deliberately boring.

## Fan-out: when one category is too big for one pass

The case that forces it: a lopsidedly full `trade/`, where the category seat hits exactly the
shape the whole-library seat hit. It may take on the personas of its workers and go do the work —
that part is not hard. Doing it **in parallel** is where the questions are, and there are four
rules.

**1. The branch is the lock.** A seat's work lives on one orphan branch. Parallelism *inside* a
seat must never mean two writers on `advocate/trade`. Everything below follows from refusing
that one thing.

**2. Fan out on reading; serialize the writing.** Workers take a slice, read, and return
findings. **The seat writes once, at the end, on its own branch.** No merge, no reconciliation, no
new state machine — and a worker that returns nothing costs a slice rather than a round.

**3. Slices are derived from the tree, not from the pool size.** Directory order plus the cursor.
The same category at the same cursor produces the same partition whether the budget bought two
workers or five. **A partition that depends on how many workers you could afford is not
reproducible**, and an unreproducible partition makes a crashed round unrecoverable — you cannot
tell which slice was lost.

**4. The cursor is the only checkpoint.** Per-worker state is scratch and is not kept. If a
worker dies its slice was never written, the cursor never passed it, and the next round serves
it.

## Two of the same seat at once: refuse, do not orchestrate

**Two *different* category seats running in parallel is the good case, and it costs nothing.**
Different branches, disjoint subtrees, no shared state, separate budgets. That is the
parallelisation worth having, and **it is what splitting by category actually buys** — not one
agent under less strain, but two concerns that were never one.

**Two runs of the *same* seat is not an orchestration problem. It is a lost update.** Two
sessions preparing the same workspace and writing the same branch will silently drop one of
them, and no amount of budget arithmetic makes that safe. The second should **decline**: the
workspace is claimed, or the branch moved after the round began.

Worth being precise about the difference from the machine's existing idiom. The workload board
on this machine is **an announcement, not a lock** — two agents may both claim and both proceed,
and the point is only that each can see the other. That is right for *"I am about to use the
CPU."* **A seat round is stricter, because it writes**, and a writer that can see another writer
and proceeds anyway has not been helped by seeing it.

## What a round may not do

- **Read held content it was not granted.** Above. A round that "checked what a project's
  instructions said" has spent its budget doing the one thing it must not.
- **Write anywhere but its own branch.**
- **Spend another category's budget**, including by noticing something next door and following it.
- **Promote a word to a category**, or retire a reserved one. Proposing is welcome;
  [`CATEGORIES.md`](CATEGORIES.md) says why taking is not.
- **Answer a question with a scan.** If what a category holds cannot be answered from the
  library's own documentation, **the documentation is what needs work** — not the question.

## Where seats are declared

**This engine declares no category seat of its own, and that is correct:** it holds no category.
It reserves the words and writes the health definitions, which is the part every library shares.

**An operator's library declares its own**, in its own `advocate.yml`, one per category it
actually holds *and* wants tended — which is fewer than it holds. [`OPEN.md` §7](OPEN.md) already
records that seating is the operator's act and that a seat whose constituency was guessed is
worse than an empty chair. Nothing here changes that; it only means the next person opening
`advocate.yml` has the category rows to start from instead of a blank page.
