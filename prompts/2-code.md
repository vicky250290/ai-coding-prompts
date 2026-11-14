# Code

Match the mode to the task: autocomplete for the line you were about to write, chat for one function or one migration, agents for mechanical sweeps with a clear finish line. **The more judgement a task needs, the smaller the batch should be.**

## Skeleton first

```text
Propose function signatures and file layout only — no implementations —
for [feature]. [stack].
```

Agree on types, signatures and files before any function bodies. Then implement one unit at a time: implement, read, run, commit at every green point.

## Match your conventions

```text
Here's an existing file from our codebase. Follow its patterns exactly when
writing [new thing].
```

A real file is unambiguous where a prose style guide is vague. This one habit kills most convention drift.

## Refactor safely

```text
Extract [pieces] into separate functions. Keep the public signature
identical. Don't change behaviour, including [deliberate quirk]. Show me
the diff.
```

Naming the deliberate quirk matters: otherwise the model "fixes" it.

## Understand legacy code

```text
Explain what this function does, what calls it, what it assumes about its
inputs, and what would break if I changed [X].
```

## Read every block before you run it

1. Does it do what I asked, not what it decided would be nicer?
2. What did it invent? Check that every import and method actually exists.
3. Where does it break? Empty, null, zero, negative, enormous, concurrent.
4. Can I explain every line? If not, learn it or delete it.

**Two-strikes rule:** if the second attempt at the same fix didn't work, the third won't either. Reset with a fresh framing, or write it yourself.
