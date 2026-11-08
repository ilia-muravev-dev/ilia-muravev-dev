# Ilia Muravev

**Backend engineer · Java & Kotlin · 3+ years in production**

I build backend services that have to stay fast and correct under load: databases, messaging and
reporting. I've worked on a queue-management system for a retail bank's ~140 branches, a fleet
telematics and dispatch platform, and — currently, at Perfema — an EdTech SaaS where I own features
end to end, from Kotlin/Java services to the React screens on top of them.

**Looking for** backend or full-stack roles in fintech or other high-load, data-heavy products —
remote, hybrid or relocation; employment or B2B.
[LinkedIn](https://www.linkedin.com/in/ilia-muravev/) · ilia.muravev.dev@gmail.com ·
English C1, Russian native

## Problems I've solved at work

The code is private, the numbers are from production.

- **A slow aggregate endpoint** — replaced an N+1 walk over the organisation tree with a recursive CTE,
  a partial index and DTO projections: p95 **1.8 s → 236 ms**, pool waits 18 → 0, ~2,300 rps sustained
- **Duplicate emails** — moved notifications onto a transactional outbox with a natural dedupe key:
  **~9 duplicates a week → 0**, and nothing lost on a crash between commit and send
- **Tables growing by ~7M rows a month** — monthly partitioning with scheduled creation and retention:
  a month of data **3.4 s → 290 ms**
- **Nightly sync between two databases** — Debezium CDC with idempotent, versioned upserts:
  replication lag **hours → seconds**
- **Analytics on the transactional database** — a ClickHouse reporting layer fed from the event
  stream: a 30-day fleet report **~38 s → 2.4 s**
- **Per-request user lookups** — Keycloak 26 with custom SPI (protocol mapper + user storage
  provider) putting the domain user and roles into the JWT: average response time **~18 ms lower**
- **Bank reports timing out** — a dedicated pool with statement timeouts and streamed exports:
  **~15 gateway timeouts a week → 0**

## Public projects

Built the way I work: one command to run, CI on every push, a test for every claim.

**[ledger](https://github.com/ilia-muravev-dev/ledger)** — a double-entry payments ledger
(Java 21, Spring Boot, PostgreSQL, jOOQ, Kafka, React). Idempotent transfers; pessimistic and
optimistic locking behind one interface, with the same concurrency tests and a benchmark for both;
a transactional outbox to Kafka and a read model that tolerates duplicates and reordering;
multi-currency transfers; k6 load tests and a Grafana dashboard. Under load it hit a PostgreSQL bug
that is fixed upstream but not yet released — reproduced in plain SQL and worked around
([#26](https://github.com/ilia-muravev-dev/ledger/issues/26)).

- **[slotlock](https://github.com/ilia-muravev-dev/slotlock)** — a booking API that cannot double-book,
  five locking strategies raced under k6 (TypeScript, NestJS, PostgreSQL)
- **[single-flight-auth](https://github.com/ilia-muravev-dev/single-flight-auth)** — an npm library
  that refreshes an access token once across all browser tabs
- **[second-opinion](https://github.com/ilia-muravev-dev/second-opinion)** — a pull-request reviewer
  that verifies its own findings and is scored on PRs with planted defects
- **[fieldwise](https://github.com/ilia-muravev-dev/fieldwise)** — document extraction with a per-field
  evaluation harness

## Stack

**Java 17/21, Kotlin** · Spring Boot, Spring Security, JPA/Hibernate, jOOQ, JdbcTemplate, Ktor ·
**PostgreSQL**, ClickHouse, Redis, Flyway · **Kafka**, RabbitMQ, ActiveMQ Artemis, Debezium ·
Keycloak, OAuth2/OIDC · Docker, Kubernetes, GitLab CI · Prometheus, Grafana, OpenTelemetry, k6 ·
JUnit 5, Testcontainers · React, TypeScript
