# 30-minute pre-launch security routine

You don't need a pentest to catch the big stuff. Run this before every launch and after any big change.

- [ ] **Secrets (5 min):** open the live site, F12 → Sources, search the loaded scripts for `sk_live`, `service_role`, `secret` and `AKIA`. Any match is exposed: move it server-side and rotate it.
- [ ] **Database rules (5 min):** Supabase → Database → Security Advisor shows tables without RLS; enable it everywhere. Replace Firebase "test mode" rules.
- [ ] **IDOR (5 min):** log in as user A, copy a request like `/api/orders/1001` from the Network tab as cURL, change the ID, re-run. Someone else's data = broken.
- [ ] **Payments (3 min):** prices are decided on the server; webhooks verify the signature over the raw body.
- [ ] **Dependencies (3 min):** `npm audit`, and look up every AI-suggested package on npmjs.com.
- [ ] **Headers and errors (3 min):** check your grade on securityheaders.com; make sure errors don't show stack traces.
- [ ] **Spend cap (3 min):** set a hard monthly limit in your AI provider's dashboard.
- [ ] **Backups (3 min):** confirm backups work and dev and prod are separate.

If you handle health, financial or children's data, or a breach would sink the business, also pay for a professional review.

---

Explained step by step in [Vibe-Coded App Security: A 30-Minute Pre-Launch Checklist](https://www.techbrosebooks.co.in/blog/vibe-coded-app-security-checklist?utm_source=github&utm_medium=referral&utm_campaign=ai-coding-prompts).
