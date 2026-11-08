# Ilia Muravev

Backend engineer · Java, Kotlin · 3+ years in banking, fleet telematics and EdTech.

Open to backend or full-stack roles in fintech and high-load products — remote, relocation or B2B.

## Selected work

- Real-time vehicle positions over WebSocket, filtered by map viewport and access rights, for hundreds of concurrent connections
- Real-time dashboards for a bank's ~140 branches: queue state, waiting and service times, operator workload, drill-down to a single ticket, regional time zones
- Bank report timeouts **~15/week → 0**: dedicated connection pool, statement timeouts, streamed exports
- Write-endpoint p95 **−37%** by moving event fan-out to a bounded executor with caller-runs back-pressure
- Reliable JMS flows: idempotent consumers, redelivery with backoff, DLQ with queue-depth alerts
- Team observability: Micrometer, OpenTelemetry tracing, structured logs into Loki, Grafana dashboards and alerts

## Projects

- **[ledger](https://github.com/ilia-muravev-dev/ledger)** — double-entry payments ledger: idempotent transfers, pessimistic vs optimistic locking, Kafka outbox, FX, k6 (Java, Spring Boot, PostgreSQL)
- **[slotlock](https://github.com/ilia-muravev-dev/slotlock)** — booking API that cannot double-book, five locking strategies raced under load (TypeScript, NestJS)
- **[single-flight-auth](https://github.com/ilia-muravev-dev/single-flight-auth)** — npm library: one token refresh across all browser tabs
- **[second-opinion](https://github.com/ilia-muravev-dev/second-opinion)** — PR reviewer scored on pull requests with planted defects
- **[fieldwise](https://github.com/ilia-muravev-dev/fieldwise)** — document extraction with a per-field evaluation harness
- **[Chorelet](https://apify.com/chorelet)** — public-data scrapers on Apify (apps, jobs, markets, events, social) that I build and run

## Stack

Java · Kotlin · Spring Boot · PostgreSQL · ClickHouse · Kafka · RabbitMQ · Debezium · Keycloak · Docker · Kubernetes · Prometheus · Grafana · Testcontainers · React · TypeScript

[LinkedIn](https://www.linkedin.com/in/ilia-muravev/) · ilia.muravev.dev@gmail.com
