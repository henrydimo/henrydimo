# Henry Dimobika

I work at the intersection of product and engineering: I take production gaps, QA findings, and partner needs and ship them as working product — UI, APIs, and the operational tools in between.

Most of my recent work is in a **private production codebase** ([Awasource](https://awasource.com)): a hiring platform for companies and talent, with assessments, partner distribution, and operator tooling. The source is not public. This page is the public record of what I have been building there. Happy to walk through the product and the diffs on a call.

## Recent work (Awasource)

**Partner platform.** Shipped the partner API service end to end: a login-only portal for signed partners, single key-pair lifecycle (provision, reveal-once, rotate with a Stripe-style grace window, revoke) with secrets stored as peppered HMAC hashes, a versioned public REST API, HMAC-signed idempotent webhooks with backoff retries, and a cron sweep that retires rotated keys. Partners run our psychometric assessments over the API — real rubric-weighted scoring, not a stub — plus candidate-fit endpoints, shared enrollment links, and a candidate test portal. Also built the operator admin for provisioning partners and keys, and a compatibility layer so the backend serves the exact contract a teammate's merged frontend expected.

**Assessment engine.** Built the psychometric assessment catalogue behind the platform: 59 live roles across Technology & Digital, Business & Finance, Creative & Design, and Sales & Operations — roughly 1,770 items on a shared question taxonomy, with AI-usage judgement woven into the scenarios so each test probes how a candidate actually uses AI in that role. Paired with per-role scoring rubrics and an OpenAI-backed scoring service with a heuristic fallback.

**Backend architecture and performance.** Set the backend on a strict thin-controller pattern over `BaseService`/`BaseController` base classes, refactored monolithic service/model files into separated layers (including splitting the credit model into one-time and annual packs), and caught and fixed a cluster of critical bugs during deep review sessions. Root-caused chronic `job.create` timeouts — unindexed regex scans forcing full collection scans, in-memory similarity over unbounded sets, and dozens of inline model calls per request — and introduced a `withTimeout`/`runStep` pattern with trace IDs and non-fatal warning collection, alongside a queue-backed fix path.

**Trust and compliance.** Region-aware KYC so non-Nigeria clients are not forced through NG-only fields (and NG clients still get the right ones). Integrity signals on assessments so operators and clients can see when a result may not be reliable.

**Email and lifecycle.** A real automation system instead of a stub: templates, merge fields resolved against live talent/client data, event scoping, last-day cron, delivery search and dashboards, currency-aware variants (including NGN from signup context), and transactional template fixes. Designed and built the operator-facing screens — an automation flow list and a trigger-setup drawer — and added observability so delivery can be traced in production.

**Operator and marketplace QA.** Admin client records, invite links, hiring stats after team-invite accept, job-listing close flows, support threads clients and talents can continue, and search/status cards on talent and client delivery history.

Stack on this work: **React**, **Redux**, **Node/Express**, **MongoDB**, **Redis/Bull**, plus the usual production glue (auth, templating, object storage).

## How I work

I stay close to the product: reproduce the bug, fix the contract (API + UI), and leave the operator able to see what happened. I lean heavily on AI in the loop — **Claude** for architecture, backend implementation, debugging, and scoping — but I still own the Git author, the PR, and whether it is safe to merge. The AI accelerates the work; the engineering judgement, the review, and the call to ship are mine.

## Contact

GitHub: [henrydimo](https://github.com/henrydimo)

If you are reviewing this for a role, the useful next step is a 20-minute screen share of the admin, partner, and automation surfaces — not a public clone of the repo.
