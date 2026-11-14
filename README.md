# AI Coding Prompts

Copy-paste prompts for coding with AI assistants (Claude Code, Cursor, Copilot, Codex, Lovable, Bolt), organised by stage: **plan, code, test, review, deploy, debug**, plus a **security pass** to run before you launch anything AI-built.

They work with any model. Replace the `[brackets]` with your details.

## The one rule behind all of them

> If you can't verify the output in five minutes, you asked for too much.

Ask for small, checkable pieces, give the model your real context (schema, error text, an existing file to copy), and verify after every stage. A made-up requirement caught in planning costs a minute; caught in production it costs an afternoon.

## Contents

| File | What's in it |
|---|---|
| [prompts/1-plan.md](prompts/1-plan.md) | Surface unknowns, harvest edge cases, compare trade-offs |
| [prompts/2-code.md](prompts/2-code.md) | Skeleton first, match your conventions, refactor safely, understand legacy code |
| [prompts/3-test.md](prompts/3-test.md) | Tests from the spec (not the code), find coverage gaps |
| [prompts/4-review-deploy-debug.md](prompts/4-review-deploy-debug.md) | Self-review a diff, write the PR description, debug with ranked hypotheses |
| [security/fix-it-prompts.md](security/fix-it-prompts.md) | 10 prompts that find and fix the most common holes in vibe-coded apps |
| [checklists/pre-merge.md](checklists/pre-merge.md) | Run over anything AI helped write, before the PR |
| [checklists/pre-launch-security.md](checklists/pre-launch-security.md) | The 30-minute security routine before you launch |

## Where these come from

The coding prompts and the pre-merge checklist are the appendix of **[The Vibe Coding Playbook](https://www.techbrosebooks.co.in/books/vibe-code-playbook?utm_source=github&utm_medium=referral&utm_campaign=ai-coding-prompts)**, which walks through the whole plan → code → test → deploy loop, including a 90-minute worked example building a feature end to end.

The security prompts come from **[Ship Your Vibe-Coded App Without Getting Hacked](https://www.techbrosebooks.co.in/books/ship-your-vibe-coded-app-without-getting-hacked?utm_source=github&utm_medium=referral&utm_campaign=ai-coding-prompts)**, which pairs each one with a hands-on check to confirm the hole is really closed, plus a full audit of a sample Lovable + Supabase + Stripe app.

Free articles:
- [A Vibe Coding Workflow That Ships: Plan, Code, Test, Deploy](https://www.techbrosebooks.co.in/blog/vibe-coding-workflow-plan-code-test-deploy?utm_source=github&utm_medium=referral&utm_campaign=ai-coding-prompts)
- [Vibe-Coded App Security: A 30-Minute Pre-Launch Checklist](https://www.techbrosebooks.co.in/blog/vibe-coded-app-security-checklist?utm_source=github&utm_medium=referral&utm_campaign=ai-coding-prompts)

## Contributing

Found a prompt that works better? Open an issue or PR with the prompt, what you used it for, and what changed in the output.

## License

[MIT](LICENSE). Use them anywhere, including at work.
