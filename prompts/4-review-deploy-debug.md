# Review, deploy, debug

## Self-review before a human sees it

```text
Review this diff as a senior engineer on this codebase. Focus on
[concerns]. Cite line numbers. Skip style nits.
```

For example, `[concerns]` = unhandled error paths, race conditions, N+1 queries, missing validation. **Leave out "skip style nits"** and you get twelve comments about variable names and nothing about the transaction you forgot to roll back.

The model is good at null paths, off-by-one errors and unclosed resources. It's blind to whether the feature is a good idea, which is why humans stay in the loop.

## PR description

```text
Write a PR description from this diff: what changed, why, how to test
manually, risk and rollback. Under 200 words. No marketing language.
```

## Debug with hypotheses, not answers

```text
Given these logs and this recent diff, rank the likely root causes by how
well they fit the timing. For the top one, give me a command that would
confirm or rule it out.
```

Asking for a confirming command turns a confident guess into something you can check in a minute.

**Scrub logs first:** remove emails, tokens and account IDs before pasting them into any AI tool.
