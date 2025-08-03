# Monitoring Stack with Prometheus + Grafana (Alerting Included)

![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=Prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=Grafana&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white)

A production-ready monitoring stack for infrastructure and applications, featuring:
- **Prometheus** for metrics collection
- **Grafana** for visualization
- **Alertmanager** with pre-configured alert rules
- **Loki** for log aggregation (optional)

##  Quick Start

### Prerequisites
- Docker 20.10+
- Docker Compose 2.2+
- 2GB RAM (minimum)

### Installation
```bash
git clone https://github.com/pankajaswal888/observability-stack.git
cd observability-stack
docker-compose up -d

 Configuration
1. Prometheus Targets
Edit prometheus/prometheus.yml to add scrape targets:

scrape_configs:
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']

2. Alert Rules
Modify prometheus/alert_rules.yml:

groups:
- name: instance-down
  rules:
  - alert: InstanceDown
    expr: up == 0
    for: 5m
    labels:
      severity: 'critical'

3. Grafana Dashboards
Pre-configured dashboards are in grafana/provisioning/dashboards/. Add your own JSON dashboards here.

 Alerting Setup
Configure receivers in alertmanager/config.yml:

receivers:
- name: 'slack'
  slack_configs:
  - api_url: $SLACK_WEBHOOK_URL
    channel: '#alerts'

Docker Compose Overview
services:
  prometheus: # Metrics collection
  grafana:    # Visualization
  alertmanager: # Alert routing
  loki:       # Log aggregation (optional)
  promtail:   # Log collector (optional)

Add Monitoring Targets:

Node Exporter for host metrics

cAdvisor for containers
