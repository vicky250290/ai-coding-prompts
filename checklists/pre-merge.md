# Pre-merge checklist

Run this over anything AI helped you write, before you open the PR.

## Correctness
- [ ] I have read every line and can explain each one
- [ ] Every import, method, and config key actually exists
- [ ] It does what I asked, not what it decided would be nicer
- [ ] Empty, null, zero, negative, and very large inputs are handled

## Tests
- [ ] Tests derive from the spec, not from the implementation
- [ ] Boundary cases present, with hardcoded expected values
- [ ] I broke the code on purpose and a test went red
- [ ] Assertions check results, not just that a function was called

## Security
- [ ] No secrets, keys, or real customer data in the code, tests, or my prompts
- [ ] Any new dependency verified as real, maintained, and intended
- [ ] Auth, crypto, and access control use established libraries and have human review
- [ ] User-supplied input is validated and escaped at the boundary

## Fit
- [ ] Follows the conventions in our rules file
- [ ] Error handling matches the rest of the codebase
- [ ] No stray dependencies, dead code, or commented-out experiments
- [ ] Someone on-call at 3am could follow what this does

---

From **[The Vibe Coding Playbook](https://www.techbrosebooks.co.in/books/vibe-code-playbook?utm_source=github&utm_medium=referral&utm_campaign=ai-coding-prompts)**.
