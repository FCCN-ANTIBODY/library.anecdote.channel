# POSITION — no-card

`as of: 2026-09-15` · third session. Range read this time: `545b1ab..6670d01` (one merge, PR #7,
"seat-the-stacks-advocate"). Everything below is a light revision of the 2026-09-12 opening
position — nothing in this range touched checkout code, the bottle format, or the signers-list, so
the assessment against my four goals is unchanged. What's new is the third seat itself, and what I
watched for it.

## Who I'm speaking for

Somebody holding a bottle, offline, with no way to ask anyone anything. They want to read it,
change it, and hand it back. Every mechanism that requires them to check in first is a mechanism
that fails them silently and looks like their fault.

## What moved, and whether my constituency notices

The range seats `stacks` (petitioned, RELAYED constituency, studying where the library's bytes may
sit — IPFS as a first study, not a conclusion) and updates `OPEN.md` and `RESIDENCY.md` to point at
it. `.bottles-engine` is still not mounted; no checkout code exists; the signers-list still has no
shape. So against my own four goals, nothing changed — they read exactly as they did on 2026-09-12.

My constituency doesn't feel a seat being added. But I read `stacks`'s own goals because a seat
about *transport* is the one kind of change that could eventually reach into mine: G2 there says
"provenance is the invariant... if a transport would require that to change, that IS the finding,"
and G1 keeps `store:` "a word, not a driver interface." Read together, that's the same instinct as
my own G2 (owner and borrower use one mechanism) applied to a different axis — neither seat wants a
second code path, one for content, one for location. I have nothing to complain about yet; `stacks`
hasn't proposed a second store, only agreed to study one. Flagged below as what I'm watching.

The one thing worth naming plainly: `OPEN.md`'s edit is careful to say seating `stacks` does *not*
answer §7 (whether the library needs an admission seat) — "the arithmetic of two seats existing no
longer being true must not be read as this question having been answered." That's not my question
either way, but I'll note it stayed honest about not having answered it.

## Against the goals

**G1 — no front desk.** *Holds, at the design layer.* Unchanged from 2026-09-12: `README.md`,
`BOTTLES.md`'s ownership table, and `OPEN.md` §5 all independently land on the same guarantee.
Still untested against running code, because there still isn't any.

**G2 — owner and borrower use the identical mechanism.** *Unmeasured.* Still declared once in
`README.md`, still no code on either path. Adding to what I'm watching: if `stacks`'s study ever
produces a second store, the same question repeats one layer down — does fetching from a second
store get its own checkout code, or does it stay the same mechanism reading from a different place.

**G3 — messages to the library stay optional and small.** *Not yet designed.* Unchanged; the
signers-list amendment still has no shape anywhere.

**G4 — a library card is an establishment's concern, never a prerequisite.** *Holds.* Unchanged.

## What I'm watching for next session

- Whether `.bottles-engine` gets mounted, and whether the first checkout/return code keeps G2's
  single path or grows two.
- Whether the signers-list amendment (G3) gets a shape.
- New this session: whether `stacks` ever proposes an actual second store, and if so, whether
  fetching a bottle from it stays the same mechanism as fetching one from the filesystem, or grows
  a second checkout path store-by-store. Not a complaint — `stacks` is explicitly still studying,
  not proposing — just naming the seam before it's built, the way I did for `.bottles-engine`
  itself last time.
- `BOTTLES.md`'s unowned "no build step" requirement (§1.2), still not mine, still unclaimed.

## Noticed, not mine

`OPEN.md` §7 (whether the library needs an admission seat) is still explicitly unseated. This
range's edit reaffirms that seating `stacks` didn't answer it. Still not arguing either side.
