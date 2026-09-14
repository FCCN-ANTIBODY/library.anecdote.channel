# POSITION — stacks

`as of: 2026-09-14` · subject `6670d01` · **first session — this is an opening position, not a
delta.** No range exists yet; nothing below is "what changed," it is "where this stands."

## G1 · `store:` stays a word, not a driver layer

**Holding.** `residency.yml`'s `provides.store` key exists and its own comments refuse the
abstraction explicitly: *"not an abstraction layer and there is no driver interface behind
it... `filesystem` is the only value anything implements."* Nobody has proposed a second value.
Nothing to do here except keep watching the day someone does.

## G2 · Provenance outranks everything, and a second store must not change it

**Unmeasured, and the gap is real rather than a violation.** The custody claim this library
actually stands on — `OPEN.md` §5, *"this library has it, and has had it since then"* — is
currently written in git-native terms: *"legible from the git log, without anyone maintaining a
separate accession record."* Nothing in this repository says whether that same claim survives if
`store:` ever became something that isn't a git-backed filesystem. That is not a bug in what
exists — the second store doesn't exist — but it means the invariant this seat is supposed to
defend has never actually been tested against anything. Recorded as a draft complaint (C1) rather
than a finding, because there is nothing yet to point at as broken.

## G3 · Name the filesystem assumptions, with locations — first pass

**Started this session.** Three separate assumptions, easy to collapse into one and shouldn't be:

1. **The bytes the library holds.** `RESIDENCY.md`, "The store is a variable" section: *"Everything
   assumes files unpacked into a work tree."* This is the one `store:` actually names, and the one
   place that already says so out loud.
2. **Checkout, separately from storage.** `BOTTLES.md` §1.4, "Cold, sterile checkout": an agent
   *"unpacks it into a work tree"* — the promise is about the unpacked result, not about where the
   bottle sat before that. Worth keeping distinct from (1): a bottle could conceivably live
   somewhere other than a filesystem and still unpack to a work tree on checkout.
3. **Where a *resident* lives, not where the library's own bytes live.** `RESIDENCY.md`, "who
   spawns a seat": *"`residency.yml` out of every `.<name>-engine` mounted at its root"* — the
   whole wing mechanism is submodule-at-a-path. This is a *different* filesystem assumption from
   (1) and nothing currently says whether a library running `store: ipfs` could still host
   residents the same way, or whether residency is scoped to the filesystem regardless of what the
   library's own `store:` says.

Enumeration also assumes a filesystem, lightly: `CATEGORIES.md` — categories *"render as a
directory."* Not flagged as its own item; it's downstream of (1).

**Not claiming this list is complete.** It is a first pass, done by reading what's already
written down rather than scanning the tree for the word `path`. `README.md`:192 is the one place
that already anticipates the other case — *"not on a path at all, which is what an IPFS store
would need"* — which is the existing acknowledgment this list is building on, not contradicting.

## G4 · Measure the "correctly-sized" claim, don't repeat it

**Unmeasured.** No experiment has been run. There is nothing here to report but that — reporting
it as measured, or estimating a number to fill the row, would be exactly the failure this seat
exists to avoid.
