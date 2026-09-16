# POSITION — no-card

`as of: 2026-09-16` · fourth session. Range read: `6670d01..5b8f333`, ten merged PRs (#8–#17,
2026-09-13). This is the largest range I've read — `GRANTS.md` alone is 399 lines — and it is the
first range that argues with my own goals by name rather than passing near them.

## Who I'm speaking for

Somebody holding a bottle, offline, with no way to ask anyone anything. They want to read it,
change it, and hand it back. Every mechanism that requires them to check in first is a mechanism
that fails them silently and looks like their fault.

## What moved, and whether my constituency notices

Ten PRs landed: `GRANTS.md` (new — what a "grant" means here and how private library content gets
read), `ADOPTING.md`/`adoption/` (a general onboarding door plus a worked fitting for a real Discord
media project), `SHELVES.md`, `EXHIBIT.md`, `PEERS.md`, `CATEGORIES.md` (new reserved-word
machinery), `OPEN.md` updates (§3/§4 answered), and a `residency.yml` peer entry for `tell`.

Most of this — categories, shelves, exhibit, the general adoption door — is health-and-discoverability
machinery my constituency doesn't feel; a borrower holding a bottle doesn't care what word names the
repository that served it. **`GRANTS.md` and the `tell` peer entry in `residency.yml` are different.
They are squarely mine**, and this is the first time the repository has done real design work on the
exact question my seat exists to watch: what happens when someone has to be let in.

### GRANTS.md: read-privilege for content the library never held plaintext

The document answers a real question — the operator wants a private library branch (git-as-OPFS,
roughly) readable from a phone via Discord auth + a passkey, so a person keeps seeing media whose
CDN links expire. `GRANTS.md`'s answer, worked through carefully:

- **Fetching stays open; reading doesn't.** The library holds ciphertext and serves it to anyone —
  it authenticates nobody. What a "grant" governs is whether the bytes you already have will decrypt,
  not whether you may have them.
- **The check is against the artifact, never a service.** A blob that fails to decrypt hasn't refused
  you — there's no decider and nothing has to be online.
- **The key travels with the person.** Minted on-device (`age`, via `anecdote.channel`'s
  `composer/age-mint.mjs`), held in non-extractable IndexedDB, gated by a passkey ceremony that
  proves presence rather than performing decryption. Discord OAuth establishes entitlement *once*;
  nothing is asked again at read time.
- Stated as a rule, not just a design choice: **"A grant may never become a prerequisite for opening
  an artifact. It governs who may read what is held; it never governs who may fetch, and it is never
  consulted at the moment of reading."**

Against my G1 (no front desk) and G4 (no card as prerequisite), this holds, and holds on purpose —
the document names both refusals explicitly and designs to keep satisfying them under encryption,
which is a harder case than the plaintext one I've been watching since 2026-09-12. I have nothing to
complain about here; if anything this is the range where the two goals got their first real stress
test and came through legible.

**The `residency.yml` tripwire is worth naming on its own.** The new `peer: tell` /
`for: [checkout-requests]` entry is `strength: optional`, and its own comment says why it must stay
that way: *"if this entry ever hardens to `required`, the no-library-card rule has been lost."* That
is my G1, written by someone else, as a self-triggering check inside the repository's own config
rather than as something only my seat would notice. I'm recording it because a warning a repository
writes against itself is worth more than one I'd have to keep raising, and because it means the
condition for my next complaint is now legible without me: I only have to watch whether that one
word changes.

**The worked fitting (`adoption/worked/artist-lockers.md`) independently confirms the premise.** It
finds a real Discord-gated project's auth check is cosmetic by construction — a static host can
decorate a gate, not enforce one — and concludes plainly: *theirs is not [a card], and the library
README already blesses it.* That's an outside case landing on my G4 in its own words, for reasons
that have nothing to do with my seat existing.

### Where G3 is genuinely unresolved, and it's the one thing I'm not letting go

`GRANTS.md` also claims something narrower and less settled: that the composer's "grant" *is* the
signers-list amendment my ASK A1 has been waiting on — *"The only real reason to talk to a library is
to ask for a specific checkout — put my name on the signers, with an expiration... A grant is that
request."*

That identification does real work for the document (it means grants aren't a new kind of
conversation with the library, just an instance of the one already sanctioned), but it leaves a
question A1 already asked unanswered rather than answering it: the apparatus behind a grant — Discord
OAuth, a WebAuthn passkey ceremony, an on-device `age` identity, IndexedDB storage, a lease, a
hash-chained chronicle — is real machinery, built for the *private, encrypted branch* case.
`GRANTS.md` never says whether an ordinary bottle's plain checkout (no encryption, no privacy need)
gets this same apparatus, a lighter one, or none at all. If it's the same path, G3's "stays small" is
now measured by something concrete and I can check it. If it's a second, lighter path for the
ordinary case, that is exactly the two-code-paths risk A1 flagged in the first place — solved for
privacy, reintroduced at the boundary between the private and plain cases. Recorded in `ASKS.md`
rather than decided here; nothing in this range resolves it either way.

## Against the goals

**G1 — no front desk.** *Holds, and stress-tested.* `GRANTS.md`'s whole design is built to keep this
true under encryption, the hardest case yet, and it names the refusal explicitly rather than leaving
it implicit. `ADOPTING.md` also now restates it verbatim for new adopters.

**G2 — owner and borrower use the identical mechanism.** *Still unmeasured.* No checkout code exists
yet in this range either. Unchanged from every prior session.

**G3 — messages to the library stay optional and small.** *Partially shaped, not yet measured.* This
range is the first time the signers-list amendment got any shape at all — but only for the
private/encrypted case, and via a substantial apparatus. Whether the ordinary case shares that
mechanism or diverges from it is the open question above, and I'm treating it as the thing to watch
next rather than as settled either way.

**G4 — a library card is an establishment's concern, never a prerequisite.** *Holds.* Reinforced this
range by `GRANTS.md`'s explicit rule and by the artist-lockers fitting landing on the exact same
distinction independently.

## What I'm watching for next session

- Whether ordinary (non-private) bottle checkout ever gets its own signers-list-amendment code, and
  whether it reuses `GRANTS.md`'s apparatus or diverges from it. This is now the sharpest form of A1.
- The `residency.yml` `peer: tell` / `checkout-requests` entry: still `strength: optional`. If it
  ever hardens to `required`, that is a G1 complaint on the spot — the file already says so.
- Whether `.bottles-engine` gets mounted, and whether the first real checkout/return code keeps G2's
  single path or grows two.
- Whether `stacks` ever proposes an actual second store, and if fetching from it stays one mechanism
  or grows a second per store. Unchanged from last session; nothing in this range touched it.
- `BOTTLES.md`'s unowned "no build step" requirement, still unclaimed, still not mine.

## Noticed, not mine

`OPEN.md` §7 (whether the library needs an admission seat) is still explicitly unseated; this range
didn't touch it. `OPEN.md` §10 (a project holding obligations under more than one category at once)
and §11 (what a library exhibits when it can't serve a README) are new open questions this range, and
both read as `stacks`'s or a future seat's, not mine — flagging only because they're new, not because
I have a stake.
