# Ilia Muravev

Full-stack engineer (Python · TypeScript) who likes the unglamorous parts: the race condition, the
webhook that arrives twice, the prompt that needs a number next to it. Four repositories below,
built the same way — one command to run, green CI, a test for every claim, and every number in a
README written by the code that measured it.

| | What it is | The claim, and how it is proven |
| --- | --- | --- |
| [**single-flight-auth**](https://github.com/ilia-muravev-dev/single-flight-auth) · [npm](https://www.npmjs.com/package/single-flight-auth) | Zero-dependency TypeScript library: one access-token refresh per tab *and across tabs* (Web Locks, `localStorage` lease fallback, BroadcastChannel), ~2.3 kB | Playwright opens five tabs against a rotating-refresh-token mock server: 5 refresh calls and 4 tabs logged out without it, 1 call and 0 logouts with it |
| [**fieldwise**](https://github.com/ilia-muravev-dev/fieldwise) | Schema-driven document extraction (FastAPI, vision model with structured output, pgvector few-shot retrieval, Next.js review UI) with a per-field eval harness on the public CORD receipts | Prompt v1 → v2 on 20 held-out receipts: strict field accuracy 84.5 % → 91.1 %, value accuracy 86.3 % → 95.1 %, from committed eval reports; CI re-scores recorded model responses against a baseline |
| [**slotlock**](https://github.com/ilia-muravev-dev/slotlock) | A reservation API that cannot double-book (NestJS, Prisma 7, Postgres 17, BullMQ): idempotency keys, webhooks ordered by provider time, expiring holds, transactional outbox | Five locking strategies behind one interface — advisory lock, `FOR UPDATE`, optimistic, `SERIALIZABLE`, GiST exclusion — raced by k6 and judged from the database: 0 double bookings each; the `naive` control double-books 18 times in 20 s |
| [**second-opinion**](https://github.com/ilia-muravev-dev/second-opinion) | A GitHub Action that reviews pull requests: deterministic checks, a model review with a strict schema, and a second pass that verifies every finding before it is posted | Scored on real pull requests with planted defects (94 cases, 21 mutation operators); the first measured prompt on a free model finds the planted line in 73 % of cases — the README carries the runner's table and says what is still unmeasured |

Things these repositories taught me, kept in their ADRs: an exclusion constraint needs
`INSERT … ON CONFLICT` or concurrent inserters deadlock on each other; a webhook's order is the
provider's clock, not the arrival; a model's knowledge of version numbers is a cutoff, not a fact;
and a number nobody can regenerate is a rumour.

Reach me at ilia.muravev.dev@gmail.com.
