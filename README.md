# Duty Monitoring Board
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)
![Loki](https://img.shields.io/badge/loki-%23FF7B42.svg?style=for-the-badge&logo=grafana&logoColor=white)

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
