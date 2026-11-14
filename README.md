# Duty Monitoring Board

A containerised observability project for monitoring infrastructure and application health with **Prometheus, Grafana, Loki, and Promtail**.

The project brings metrics and logs into one place so an operator can inspect system health, investigate application behaviour, and build a clearer picture of what is happening across a service.

## Overview

The stack is orchestrated with Docker Compose and combines metrics collection, log aggregation, and visualisation.

### Observability stack

| Component | Responsibility |
| --- | --- |
| **Prometheus** | Scrapes and stores time-series metrics and evaluates alerting rules |
| **Grafana** | Provides dashboards and a central interface for exploring metrics and logs |
| **Loki** | Aggregates and stores log data |
| **Promtail** | Collects container logs and forwards them to Loki |
| **Node Exporter** | Exposes host-level metrics |
| **PostgreSQL Exporter** | Exposes PostgreSQL metrics |
| **Nginx Exporter** | Exposes Nginx metrics |
| **Docker Compose** | Runs and manages the observability services |

## Architecture

At a high level, metrics and logs follow separate collection paths:

- **Metrics:** Exporters expose metrics for Prometheus to scrape. Grafana queries Prometheus to visualise those metrics.
- **Logs:** Promtail collects container logs and ships them to Loki. Grafana queries Loki when logs need to be explored.

```text
                 ┌──────────────────────┐
                 │       Grafana        │
                 │  Dashboards / Explore│
                 └──────────┬───────────┘
                            │
                  ┌─────────┴─────────┐
                  │                   │
            ┌─────▼─────┐       ┌─────▼─────┐
            │Prometheus │       │   Loki    │
            │  Metrics  │       │   Logs    │
            └─────▲─────┘       └─────▲─────┘
                  │                   │
          ┌───────┴────────┐     ┌────┴──────┐
          │ Exporters      │     │ Promtail  │
          │ Node / Postgres│     │           │
          │ / Nginx        │     └─────▲─────┘
          └────────────────┘           │
                                  Container logs
```

## Prerequisites

- Docker Engine or Docker Desktop
- Docker Compose v2
- Git

Check that Docker and Compose are available:

```bash
docker --version
docker compose version
```

## Getting started

1. Clone the repository:

   ```bash
   git clone https://github.com/simeonprimordial/duty-monitoring-board.git
   cd duty-monitoring-board
   ```

2. Start the stack:

   ```bash
   docker compose up -d
   ```

3. Check the running containers:

   ```bash
   docker compose ps
   ```

4. Open the service interfaces:

   | Service | Local URL |
   | --- | --- |
   | Grafana | http://localhost:3000 |
   | Prometheus | http://localhost:9090 |
   | Loki | http://localhost:3100 |

   The current documented Grafana default is `admin / admin`. Use it only for a local test environment; change the credentials before exposing Grafana beyond your machine.

## What to explore

Once the services are running:

1. Open Grafana and inspect the available dashboards.
2. Check that Prometheus is scraping the configured metric targets.
3. Use Grafana Explore to query metrics from Prometheus.
4. Explore container logs through the Loki data source.
5. Compare host, database, and Nginx telemetry to understand service behaviour.

## Useful commands

| Task | Command |
| --- | --- |
| Start services | `docker compose up -d` |
| View service status | `docker compose ps` |
| Follow all service logs | `docker compose logs -f` |
| Follow one service's logs | `docker compose logs -f <service>` |
| Restart the stack | `docker compose restart` |
| Stop and remove containers | `docker compose down` |

To stop the stack and remove named volumes as well (which may delete stored metrics and logs):

```bash
docker compose down -v
```

## Troubleshooting

- **A service is not running:** Check `docker compose ps` and inspect its output with `docker compose logs <service>`.
- **A dashboard has no data:** Confirm the relevant Prometheus target is healthy and that Grafana's data source is configured correctly.
- **Logs are missing:** Check that Promtail is running, can access the intended container logs, and can reach Loki.
- **A port is already in use:** Stop the process using the port or change the relevant port mapping in the Compose configuration.

## Project goals

This project demonstrates practical observability workflows relevant to **DevOps and Site Reliability Engineering (SRE)**:

- Deploying a multi-service monitoring stack with Docker Compose
- Collecting infrastructure and service metrics
- Centralising container logs
- Exploring telemetry through Grafana
- Troubleshooting monitoring pipelines and service health

## Possible next improvements

- Add and document actionable Prometheus alert rules.
- Provision Grafana data sources and dashboards from version-controlled files.
- Add service-level indicators such as request rate, error rate, and latency.
- Document test scenarios and include screenshots of working dashboards.
- Add health checks and persistent storage configuration where appropriate.

## Repository

[View the source code](https://github.com/simeonprimordial/duty-monitoring-board)

---

Built as a hands-on observability project focused on infrastructure monitoring, metrics, logs, and operational visibility.
