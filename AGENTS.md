# Working in this repository

**It is a stub.** Read `README.md`, then `OPEN.md`, then the design it came from:
`civic-node/docs/proto-issues/library-the-knowledge-kind.md`.

## The rules most likely to be broken here

1. **A category is not an engine.** Do not add machinery because a category name suggested it.
2. **No library card.** Anything that makes lending depend on this software being up, reachable, or
   asked first is wrong. The bottle spec does the work; this repo enumerates and admits.
3. **No front desk.** Nothing here adjudicates whether a change to a bottle is allowed.
4. **Do not resolve `OPEN.md` §1 locally.** Whether `library` subsumes `bottles` touches D4 and D11
   and belongs in `anecdote.channel/docs/decisions.md`.

## Conventions

Branch from an up-to-date `origin/main`, never commit to `main`, open a PR. Keep a `.pr` file at the
repo root holding what the PR would say — and **empty it in the same act that opens the PR**, because
it is a slot and not an archive.
