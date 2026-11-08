# Ilia Muravev

Backend engineer — **Java · Kotlin · Spring Boot · PostgreSQL · Kafka**. Three years on production
systems in banking, fleet telematics and EdTech, on the parts that have to stay fast and correct under
load: data, messaging and reporting.

My work code is private. The repositories below are public projects that reproduce the problems I solve
at work, built the same way: one command to run, green CI, a test for every claim, and every number in
a README measured by code in the repository.

### [ledger](https://github.com/ilia-muravev-dev/ledger) — double-entry payments ledger

Java 21 · Spring Boot 3 · PostgreSQL · jOOQ · Kafka · Testcontainers · k6 · Prometheus/Grafana · React

- Idempotent transfers: the key is claimed under a unique index before any account lock, so 20
  concurrent requests with one key move money once
- Pessimistic (ordered `FOR UPDATE`) and optimistic (versioned, jittered retries) engines behind one
  interface, the same concurrency tests run against both, and a benchmark of the trade-off.
  Removing the lock order makes the tests fail with `deadlock detected`
- Transactional outbox → Kafka → a statement read model that tolerates duplicates and reordering;
  multi-currency transfers through FX position accounts with a stored rate snapshot
- Load-tested at 365 req/s with 0 % errors; the first run showed the read model 30 s behind, fixed with
  set-based batch projection (p99 lag 0.24 s)
- Found a PostgreSQL internal error (`new multixact has more than one updating member`) under
  contention and worked around it — written up in [#26](https://github.com/ilia-muravev-dev/ledger/issues/26)

### More

| | What it is | How the claim is proven |
| --- | --- | --- |
| [**slotlock**](https://github.com/ilia-muravev-dev/slotlock) | The same concurrency focus in a booking domain (NestJS, Prisma, Postgres, BullMQ): a reservation API that cannot double-book, with idempotency keys, ordered webhooks, expiring holds and an outbox | Five locking strategies — advisory lock, `FOR UPDATE`, optimistic, `SERIALIZABLE`, GiST exclusion — raced by k6 and judged from the database: 0 double bookings each; the `naive` control double-books 18 times in 20 s |
| [**single-flight-auth**](https://github.com/ilia-muravev-dev/single-flight-auth) · [npm](https://www.npmjs.com/package/single-flight-auth) | Zero-dependency TypeScript library: one access-token refresh per tab *and across tabs* (Web Locks, `localStorage` lease fallback, BroadcastChannel) | Playwright opens five tabs against a rotating-refresh-token server: 5 refresh calls and 4 tabs logged out without it, 1 call and 0 logouts with it |
| [**second-opinion**](https://github.com/ilia-muravev-dev/second-opinion) | A GitHub Action that reviews pull requests: deterministic checks, a model review with a strict schema, and a second pass that verifies every finding | Scored on real pull requests with planted defects (94 cases, 21 mutation operators), with precision and recall in the README |
| [**fieldwise**](https://github.com/ilia-muravev-dev/fieldwise) | Schema-driven document extraction (FastAPI, structured model output, pgvector, Next.js review UI) with a per-field eval harness | Strict field accuracy 84.5 % → 91.1 % between prompt versions on held-out receipts, from committed eval reports |

### Stack

**Backend:** Java 17/21, Kotlin, Spring Boot 3, Spring Security, JPA/Hibernate, jOOQ, JdbcTemplate, Ktor ·
**Data:** PostgreSQL, ClickHouse, Redis, Flyway · **Messaging:** Kafka, RabbitMQ, ActiveMQ Artemis,
Debezium CDC, transactional outbox · **Security:** Keycloak (custom SPI), OAuth2/OIDC ·
**Ops:** Docker, Kubernetes, GitLab CI, GitHub Actions, Prometheus, Grafana, OpenTelemetry, k6 ·
**Frontend:** React, TypeScript

Things these repositories taught me: lock in one global order or concurrent transfers deadlock; an
exclusion constraint needs `INSERT … ON CONFLICT` or concurrent inserters deadlock on each other; a
consumer that is correct can still be the bottleneck; and a number nobody can regenerate is a rumour.

[LinkedIn](https://www.linkedin.com/in/ilia-muravev/) · ilia.muravev.dev@gmail.com · open to remote,
relocation and B2B
