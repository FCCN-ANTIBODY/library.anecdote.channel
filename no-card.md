# Seat · no-card

`advocate/no-card` · last spoke **2026-09-16** · 4 session(s) · 2 draft · 0 ready

<sub>Copied whole from the branch, which is the authority. Do not edit this page — it is
overwritten every round.</sub>

## Position

### POSITION — no-card

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

## Complaints

### COMPLAINTS — no-card

Carried forward across sessions. A complaint is a felt problem in the constituency's voice, never
a proposed fix.

None yet. First session (2026-09-12): nothing is built against my constituency yet —
`.bottles-engine` isn't mounted, there's no checkout code, no signers-list mechanism. A borrower
can't feel friction from a mechanism that doesn't exist. Writing a complaint now would mean
inventing testimony for an interaction nobody has had. See `POSITION.md` for what's declared but
untested, and `ASKS.md` for the one gap worth naming ahead of the code landing.

Reviewed 2026-09-15 (range `545b1ab..6670d01`, seating of the `stacks` advocate): still nothing
built against my constituency. Nothing to withdraw, nothing to add.

## C1 · "Put my name on the list" turned out to need a Discord account, a passkey, and a browser that can mint keys

`status: draft` · `source: simulated` · `first said: 2026-09-16` (range `6670d01..5b8f333`)

I have the bottle. I don't have Discord, or my phone isn't the one with the passkey, or I'm on a
machine that's never seen either. I was told the only thing this library would ever ask of me was
small — put my name on a list, with an expiration. Now the shape of that ask, at least for the
private case, is: authorize through a platform account, complete a passkey ceremony, and let a
browser mint and store a key I'll never see. That's not nothing to ask of somebody with no way to
check in.

`GRANTS.md` itself worries about this exact failure before I do — *"a grant that feels momentous is
one somebody will avoid issuing"* — and argues the mechanism is ordinary because it's composed from
parts that already exist elsewhere, not built new. That's a real answer to *is this new
cryptography*, and it's not the same claim as *is this small to a person going through it once,
offline-capable equipment or not*. I don't know yet whether this is the ordinary case's mechanism
or a heavier one reserved for the encrypted/private branch specifically — see `ASKS.md` A1. Filed as
a draft because the range only answered the private case, and I'd be inventing testimony to say more
than that about the ordinary one.

## Asks

### ASKS — no-card

Carried forward across sessions. An ask names a target and states a shape, never a client. Once
promoted, it's cited and dropped from here.

## A1 · The bottle format needs to carry signers-amendment and owner/borrower symmetry as its own guarantees

`status: draft` · `source: observed` · `first said: 2026-09-12`

`BOTTLES.md` is this repository's own account of what it needs from a bottle engine, written as a
consumer's requirements (§1.1–1.4: small stored rendering, a build-free player, stuffing, cold
sterile checkout). Two things this seat cares about aren't in that list at all:

- **The signers-list amendment** — the one message a borrower may need to send — has no shape
  anywhere (`OPEN.md`, "Related, elsewhere": "No shape yet; must stay optional and stay small").
- **Owner-update and borrower-return as the identical operation** (`README.md`'s no-library-card
  section) is stated as a property of the *library's* mechanism, not as something the *bottle
  format itself* guarantees. If the format doesn't carry that symmetry natively, whoever writes
  the library's checkout code has to reinvent it, and a reinvented guarantee is exactly the kind
  of thing that quietly grows a second path.

**The shape:** a bottle format where amending the signers list and returning an edited bottle are
both expressed as the same kind of diff-against-a-frozen-base the format already supports for
everything else — not a special message type, and not something the library layers on top.
Target: `bottles.anecdote.channel`, once there's a wire format to check this against. Nothing to
promote yet; there's no spec surface to point at.

Reviewed 2026-09-15: unchanged. Still no wire format to check it against.

Reviewed 2026-09-16 (range `6670d01..5b8f333`): **half-answered, and only half.** `GRANTS.md` names
the composer's "grant" (Discord OAuth once, a passkey ceremony, an on-device `age` identity, a
lease, a hash-chained chronicle — all `anecdote.channel`'s machinery, not this library's) as *the*
signers-list amendment request — but only works this out for the private/encrypted-branch use case.
It does not say what an ordinary, unencrypted bottle's checkout request looks like, or whether it
shares this apparatus or gets something lighter. Still no wire format. Still targeting
`bottles.anecdote.channel` and, for the grant mechanism specifically, `anecdote.channel`'s own
decision record — this seat has no better words for either and isn't inventing any. What's new to
watch: whether the ordinary case ever gets its own answer, and whether it's one mechanism or two.
See `COMPLAINTS.md` C1 and `POSITION.md` for the reasoning.

## Last session note — 2026-09-16

### 2026-09-16

Range: `6670d015e787f6cacbbdd9b4613b804610e9f82b..5b8f33392aa4a9bad6c6827d4326e507a20a3451`, ten
merged PRs (#8–#17). Largest range so far, and the first to engage my four goals directly by name
rather than pass near them.

**What I read.** All ten first-parent merges; full text of `GRANTS.md` (new, 399 lines) and the
`OPEN.md` §3/§4 update it settles; the diff to `README.md`, `ADOPTING.md`, and `residency.yml`; the
new `peer: tell` / `checkout-requests` entry; and the relevant sections of the artist-lockers worked
fitting that `GRANTS.md` treats as its proof case. I did not read `SHELVES.md`, `EXHIBIT.md`,
`CATEGORIES.md`, `PEERS.md`, or `adoption/trade.md` in full — a keyword pass across their diffs
turned up nothing my constituency notices, and I'm trusting that pass rather than re-deriving it by
reading every line; if that's wrong, it's a gap in this session, not a claim that those files are
clean.

**What changed in the three files.** `POSITION.md` rewritten whole — G1 and G4 hold and were
stress-tested by encryption for the first time, and reinforced twice over (the `residency.yml`
tripwire, the artist-lockers finding). G3 moved from "not yet designed" to "half-shaped, and the
shaped half isn't the general case" — the first real movement that goal has had since 2026-09-12.
G2 unchanged, still unmeasured, still no code. `COMPLAINTS.md` gained one new draft, C1, about the
weight of the apparatus behind a grant, scoped honestly to what the range actually answered (the
private case) rather than extended to the ordinary case I have no evidence about. `ASKS.md` A1
updated to record the half-answer and point at exactly what's still missing.

**Tally.** 1 complaint (C1, draft), 1 ask (A1, draft, moved forward). Nothing ready, nothing
promoted, nothing withdrawn — nothing has been built long enough yet to close.

**What I deliberately didn't say.** I didn't take a position on whether the apparatus `GRANTS.md`
composes (Discord OAuth, passkey, on-device `age` identity, IndexedDB, chronicle) is *too much* —
only that I don't yet know if it's the ordinary case's mechanism or a second, private-only one, and
that distinction is what determines whether it's a complaint about weight or a complaint about a
second path. I didn't second-guess the OPFS-vs-branch correction or the WebAuthn PRF-vs-stored-key
reasoning in `GRANTS.md` — both are cryptographic/architectural judgement calls outside my
constituency's question, which is only ever "do I still need nobody's permission to open what I'm
holding." I didn't touch `OPEN.md` §10 or §11, new this range — flagged once in `POSITION.md` as
not mine and left there.

