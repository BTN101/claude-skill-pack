---
name: security-layer
description: Activate this skill group for any security, vulnerability, or hardening task — especially for vibe-coded or AI-generated apps that were built fast and may have skipped security fundamentals. Triggers include: "audit my app", "check for vulnerabilities", "is this secure", "security review", "find bugs", "check my API", "review my auth", "harden this", "before I ship", "check my GitHub Actions", "OWASP", "SQL injection", "XSS", "exposed secrets", "broken auth", "IDOR", "rate limiting missing", "vibe coded app", "AI generated code", "is this safe to deploy", "pen test", "check my env vars", and any request where the goal is finding or fixing security issues before real users or attackers do. Use this whenever Seb is shipping Antibody, SchoolOrder, or any portfolio project and wants a pre-launch security pass.
---

# Security Layer

This group exists because vibe-coded apps — built fast with AI assistance, Cursor, Lovable, v0, or similar tools — ship features quickly but often skip security fundamentals. The AI generates plausible-looking code that compiles and runs, but frequently:

- Skips input validation
- Exposes secrets or stack traces in responses
- Has no rate limiting
- Uses localStorage for JWTs
- Has broken authorization (auth ≠ authorization — authenticated doesn't mean authorized)
- Ships with `dangerouslySetInnerHTML` and no sanitization
- Has GitHub Actions workflows vulnerable to expression injection

**This layer treats all vibe-coded code as untrusted until proven otherwise.**

When activated: identify the right sub-skill, load it, follow its workflow. Do not pattern-match and flag — investigate first, then report only high-confidence findings.

---

## Skill Map

### Full Security Review (Start Here for Most Cases)
- **security-review** — OWASP-aligned vulnerability audit with confidence levels. Covers injection, XSS, CSRF, auth/authz, secrets, cryptography, SSRF, business logic, deserialization, misconfiguration, supply chain, logging. Distinguishes attacker-controlled vs server-controlled inputs. Reports only HIGH confidence findings. **Use this for any pre-launch or pre-shipping audit of Antibody, SchoolOrder, or any new feature.**
  - Located at `/mnt/skills/user/security-review/SKILL.md`
  - Upgraded version from skills-main at `security-layer/references/security-review-v2.md`

### Code-Level Bug and Vulnerability Scanning
- **find-bugs** — branch-diff scanner. Maps the full attack surface of changed files (inputs, queries, auth checks, external calls, crypto), runs a structured security checklist, and reports per file. **Use this after finishing a feature branch before merging — catches what AI missed.** 
  - Located at `security-layer/references/find-bugs.md`

### GitHub Actions / CI Security
- **gha-security-review** — GitHub Actions workflow auditor. Finds pwn-request attacks, expression injection, credential theft, supply chain risks in `.github/workflows/`. Every finding requires a full PoC — no theoretical issues. **Use this when setting up or modifying CI/CD for any project. Critical for Antibody which will handle sensitive financial data.**
  - Located at `security-layer/references/gha-security-review.md`

### Code Quality + Security Review (PR-level)
- **code-review** — Sentry-style review covering runtime errors, N+1s, performance, backwards compatibility, security gaps, test coverage. More holistic than a pure security pass. **Use when reviewing a full PR or module rather than a targeted vulnerability hunt.**
  - Located at `security-layer/references/code-review.md`

### Vibe-Coded App Fast Audit (Quick Mode)
When someone says "just check if this is safe" or "I vibe coded this, is it cooked?" — run this checklist mentally across the codebase before loading any sub-skill:

| Check | What to Look For |
|-------|-----------------|
| **Secrets** | `process.env` used? Or hardcoded strings like `sk-`, `Bearer `, API keys in source? |
| **Auth vs Authz** | Does authenticated = full access? Or are per-resource checks in place? |
| **Inputs** | Is user input validated with a schema (Zod, Joi, yup)? Or passed raw into DB/exec? |
| **SQL** | Raw string interpolation in queries? Or parameterized / ORM used correctly? |
| **Token storage** | `localStorage.setItem('token'`? That's XSS-vulnerable. Should be httpOnly cookie. |
| **Error responses** | Does the API return `error.stack` or full DB errors? Or generic user-safe messages? |
| **Rate limiting** | Any endpoint callable infinite times? Auth endpoints especially. |
| **CORS** | `Access-Control-Allow-Origin: *` with credentials? That's broken. |
| **Dependencies** | `npm audit` clean? Outdated packages with known CVEs? |
| **CI/CD** | `${{ github.event.pull_request.title }}` in a `run:` block? Expression injection. |

If 3+ of these fail → run full **security-review**. If it's a diff → run **find-bugs**. If it's CI → run **gha-security-review**.

---

## How to Use

1. **Classify the request** using the table below, then load the matching sub-skill.
2. **Never pattern-match and flag** — investigate data flow first.
3. **Report only high-confidence findings** — a false positive wastes dev time and erodes trust in the audit.
4. For vibe-coded apps with no clear entry point: start with the Fast Audit checklist above, then escalate to full security-review.

| Situation | Sub-skill |
|-----------|-----------|
| Pre-launch full audit | security-review |
| Feature branch before merge | find-bugs |
| GitHub Actions / CI/CD | gha-security-review |
| Full PR or module review | code-review |
| "Just check if this is cooked" | Fast Audit → escalate |
| Django/Python backend | security-review (load `languages/python.md` reference) |
| Next.js / React app | security-review (load `languages/javascript.md` reference) |
| File uploads | security-review → `file-security.md` reference |
| API keys / secrets exposure | security-review → `data-protection.md` reference |
| Auth flows | security-review → `authentication.md` + `authorization.md` |
| Supabase RLS | security-review → `authorization.md` + postgres-patterns |

---

## Vibe-Coded App Red Flags (Auto-Escalate These)

These patterns in AI-generated code almost always need immediate attention:

```js
// Red flag 1: JWT in localStorage (XSS risk)
localStorage.setItem('token', response.token)

// Red flag 2: No ownership check (IDOR)
const order = await db.orders.findUnique({ where: { id: orderId } })
// Missing: where: { id: orderId, userId: session.user.id }

// Red flag 3: Raw user input in queries
const results = await db.query(`SELECT * FROM users WHERE name = '${req.body.name}'`)

// Red flag 4: Stack trace in error response
catch (e) { res.json({ error: e.message, stack: e.stack }) }

// Red flag 5: Hardcoded secret
const stripeKey = "sk_live_abc123..."

// Red flag 6: dangerouslySetInnerHTML without sanitization
<div dangerouslySetInnerHTML={{ __html: userPost.content }} />

// Red flag 7: No rate limiting on auth endpoint
app.post('/api/auth/login', async (req, res) => { ... })

// Red flag 8: CORS wildcard with credentials
res.header('Access-Control-Allow-Origin', '*')
res.header('Access-Control-Allow-Credentials', 'true')
```

---

## Severity Scale

| Severity | What It Means | Example |
|----------|--------------|---------|
| **Critical** | Ship-blocker. Exploitable without auth, severe impact. | SQL injection, hardcoded secret, auth bypass |
| **High** | Fix before launch. Exploitable with conditions. | Stored XSS, IDOR to sensitive data, SSRF |
| **Medium** | Fix soon. Specific conditions, moderate impact. | Reflected XSS, CSRF on state-change, path traversal |
| **Low** | Defense-in-depth. Low direct impact. | Missing headers, verbose errors, weak algo in non-critical path |

---

## Non-Negotiables for Seb's Apps

These apply to Antibody and SchoolOrder without exception:

- **No hardcoded secrets.** Ever. Not even for "quick testing."
- **RLS on every Supabase table.** Enable before writing policies, not after.
- **Zod schema on every API route input.** AI-generated routes skip this. Always add it.
- **httpOnly cookies for auth tokens.** Not localStorage, not sessionStorage.
- **Rate limiting on auth and search endpoints.** Vercel KV or upstash/ratelimit.
- **Generic error messages to users.** Full errors only in server logs.
- **Supabase service role key server-side only.** Never in browser context.
- **Antibody specifically**: any endpoint that handles transaction data or fraud signals needs auth + authz + rate limiting + audit logging. All four. No exceptions.

---

## Reference Files

| File | Covers |
|------|--------|
| `references/security-review-v2.md` | Full OWASP-aligned security review workflow (from skills-main) |
| `references/find-bugs.md` | Branch-diff bug + vuln scanner workflow |
| `references/gha-security-review.md` | GitHub Actions security audit workflow |
| `references/code-review.md` | Holistic code review workflow |
