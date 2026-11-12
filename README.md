# Duty Monitoring Board

A SRE/DevOps project implementing a full observability stack using Docker Compose.

## Stack
- **Prometheus**: Metrics collection and alerting
- **Loki**: Log aggregation
- **Promtail**: Docker log collection
- **Grafana**: Dashboards and alert management
- **Exporters**: Node, PostgreSQL, and Nginx

## Quick Start
```bash
docker-compose up -d

## Access Points
Grafana: http://localhost:3000 (admin/admin)
Prometheus: http://localhost:9090
Loki: http://localhost:3100
