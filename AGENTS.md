# Working in this repository

**It is a stub.** Read `README.md`, then `BOTTLES.md`, then `OPEN.md`, then the design it came from:
`civic-node/docs/proto-issues/library-the-knowledge-kind.md`.

## The rules most likely to be broken here

1. **A category is not an engine.** Do not add machinery because a category name suggested it.
2. **No library card.** Anything that makes lending depend on this software being up, reachable, or
   asked first is wrong. The bottle spec does the work; this repo enumerates and admits.
3. **No front desk.** Nothing here adjudicates whether a change to a bottle is allowed.
4. **Do not resolve `OPEN.md` §1 locally.** Whether `library` subsumes `bottles` touches D4 and D11
   and belongs in `anecdote.channel/docs/decisions.md`. **Still true, and the answer has arrived
   anyway** — the operator wants `bottles.anecdote.channel` back as its own repository, so they do
   not collapse. That is recorded in §1 as a decision *arriving*, not one taken here, and the
   decision record is still owed. Do not upgrade the note into a ruling.
5. **`BOTTLES.md` is a consumer's requirements, not a spec.** If it starts describing how a bottle
   is encoded rather than what this library needs, it has drifted into somebody else's repository.
   The wire format is meant to be implementable twice, which it cannot be while it lives here.

## Conventions

Branch from an up-to-date `origin/main`, never commit to `main`, open a PR. Keep a `.pr` file at the
repo root holding what the PR would say — and **empty it in the same act that opens the PR**, because
it is a slot and not an archive.
