# Security fix-it prompts

AI writes code that *works*, not code that's *safe*, unless you ask. Veracode's 2025 GenAI Code Security Report found an OWASP Top 10 flaw in 45% of AI-generated code samples. Run these against your codebase before launch. Each one says what a correct result looks like, so you can tell whether the fix really happened.

> Paste one prompt at a time and review the diff it produces. Then **test** the fix (for example, the two-account test under prompt 3); a prompt alone proves nothing.

## 1. Map where trust decisions happen

```text
You are a security reviewer. List every place in this app where data is read
from or written to the database, sent to a third-party API, or where a user's
identity is checked. For each, tell me whether the check happens on the
server or only in the browser. Don't change code yet — just give me the map.
```

## 2. Secrets in the browser

```text
Find every secret key in this project. Any exposed to the client — prefixed
NEXT_PUBLIC_ or VITE_, or imported into browser code — must move to
a server-only environment variable used only from a server route. Show the
corrected code, then list which keys I need to rotate.
```

**Correct result:** a server route reads `process.env.OPENAI_API_KEY` (no public prefix), and the browser only calls your own `/api/...` endpoint. Then **rotate** every exposed key; deleting it from the code doesn't remove it from git history or from bundles bots already scraped.

## 3. Supabase Row Level Security

```text
For every table in my Supabase public schema, enable Row Level
Security and write policies so a user can only SELECT, INSERT, UPDATE,
and DELETE their own rows, matched on user_id against auth.uid(). Write
separate policies per operation, never USING (true). Give me the SQL.
```

**Correct result:** `ALTER TABLE todos ENABLE ROW LEVEL SECURITY;` then one policy per operation using `(select auth.uid()) = user_id`.
**Test it:** create two accounts, sign in as A, try to fetch B's row. If data comes back, the policy is broken.

## 4. "Change the ID in the URL" (IDOR)

```text
Review every route and query that takes an id from the URL, query string,
or body. Add a server-side check that the authenticated user owns that
record, inside the query itself (WHERE id = :id AND user_id = :currentUser)
rather than a separate lookup. Return 404 when the record isn't theirs.
```

**Correct result:** `db.order.findFirst({ where: { id, userId: session.user.id } })`: ownership is part of the query, and a miss returns 404.

## 5. Payments the browser controls

```text
Make my Stripe integration secure. Prices must be set server-side from a
Stripe price ID, never a client-supplied amount. My webhook handler must
verify the Stripe-Signature header using the raw body and
STRIPE_WEBHOOK_SECRET, reject invalid events with 400, and handle
events idempotently. Gate premium features on real subscription status,
checked server-side.
```

**Correct result:** the handler reads the raw body with `req.text()`, calls `stripe.webhooks.constructEvent(body, sig, secret)` in a try/catch, returns 400 on a bad signature, and only grants access after it succeeds. (Same idea for Razorpay, Paddle or any other provider: verify the signature over the raw body.)

## 6. XSS, SQL injection and prompt injection

```text
Scan for XSS and SQL injection. Wrap any dangerouslySetInnerHTML in
DOMPurify.sanitize with an allow-list of safe tags. Convert string-
concatenated SQL to parameterized queries. Keep user content separate
from system instructions in every LLM call, and never execute actions
based solely on model output.
```

**Correct result:** `db.query("SELECT * FROM notes WHERE id = $1 AND user_id = $2", [id, userId])`: input can never change the shape of the query.

## 7. Endpoints with no limits

```text
Add rate limiting to every endpoint that calls a paid API or sends email —
limit by authenticated user id (for example 5 per minute and 100 per day)
and return HTTP 429 with a friendly message when exceeded. Require
authentication on these routes. Cap the maximum input length sent to the
LLM.
```

**Correct result:** a per-user limiter runs before the AI call, and a prompt over 2,000 characters is rejected with a 400 before it reaches the API. Also set a **hard monthly spend cap** in your AI provider's dashboard.

## 8. Packages that don't exist

```text
List every third-party package this project imports and confirm each exists
on the npm registry with real usage — flag any you can't verify as possibly
hallucinated. Then run through the npm audit findings and update
vulnerable packages to safe versions without breaking the build. Show me
the changes and anything that needs manual review.
```

AI sometimes recommends packages that don't exist, and attackers register those names ("slopsquatting"). Keep it fixed with a `.github/dependabot.yml` that checks npm weekly.

## 9. Headers, CORS and error leaks

```text
Add standard security headers (Content-Security-Policy, Strict-Transport-
Security, X-Content-Type-Options, X-Frame-Options, Referrer-Policy) to
my app. Restrict CORS to my production domain only. Make sure error
responses never include stack traces or internal details — log those server-
side instead.
```

**Correct result (Next.js):** an async `headers()` function in `next.config.js` returns those headers for every route (`source: "/(.*)"`).

## 10. Final audit

```text
Act as a pre-launch security auditor. Go through my checklist against this
codebase and report pass or fail with the exact file and line for each item.
For every failure, give me the fix.
```

Paste [checklists/pre-launch-security.md](../checklists/pre-launch-security.md) as "my checklist".

---

Each prompt here has a matching detection step and a worked example in **[Ship Your Vibe-Coded App Without Getting Hacked](https://www.techbrosebooks.co.in/books/ship-your-vibe-coded-app-without-getting-hacked?utm_source=github&utm_medium=referral&utm_campaign=ai-coding-prompts)**.
