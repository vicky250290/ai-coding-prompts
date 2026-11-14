# Plan

Planning doesn't feel like progress, which is why it gets skipped. It's also the stage that pays best. Don't ask the model for a plan; ask it to interrogate you first.

## Surface the unknowns

```text
Before proposing anything, ask me the 7 questions that most affect the
design of [feature]. Number them.
```

**Why it works:** you get the questions you'd otherwise discover three days in, with the feature half built. For a recurring-expenses feature: what happens to future instances when someone deletes the series? What does a monthly rule starting on the 31st do in February?

## Edge cases

```text
List edge cases and failure modes for [feature], grouped by data, timing,
user actions, and failure recovery.
```

**Then triage them yourself** into *now*, *later* and *not doing*. That triage is your spec. On a CSV-export feature, this prompt surfaced CSV injection (a cell like `=HYPERLINK("http://evil.com","click")` becoming a live formula in Excel) before it shipped.

## Trade-offs

```text
Compare approaches A and B for [problem]. Cover [criteria]. End with which
you'd pick for a small team and why.
```

**Ask for trade-offs, never for "the answer".** You know your team and your deadline; the model doesn't.
