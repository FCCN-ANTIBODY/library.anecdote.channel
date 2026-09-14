# COMPLAINTS — stacks

## C1 · Nobody would pin mine, so it was never really there

`status: draft` · `source: simulated` · `first said: 2026-09-14`

The custody claim this library rests on — *this library has it, and has had it since then* — is
proven today by something legible from a git log. That's fine while the only store is a
filesystem. Nobody has said what proves the same claim if the bytes ever sit somewhere without a
log to read. Until someone does, the promise of custody quietly means *custody, as long as you're
on a filesystem* — and that's a narrower promise than the one written down.

## C2 · This says path in forty places and I do not have a path

`status: draft` · `source: observed` · `first said: 2026-09-14`

Three different things in this repository currently assume a filesystem, and they're not the same
assumption: where the library's own bytes sit, what checkout hands back, and where a resident's
wing lives. They read as one assumption because nothing has separated them yet. See `POSITION.md`
G3 for the first pass at where each one actually lives. Not asking for a fix — asking that the
next person who reaches for `store:` to solve one of these doesn't accidentally solve the other
two by reflex.
