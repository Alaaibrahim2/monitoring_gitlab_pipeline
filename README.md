# GitLab Pipeline Monitoring with Prometheus & Grafana

A complete DevOps monitoring project for observing GitLab CI/CD pipelines using:

* Prometheus
* Grafana
* GitLab CI Pipelines Exporter
* Custom Python Exporter
* Docker & Docker Compose

---

# Project Architecture

```text
GitLab
   |
   v
Exporters
   |
   v
Prometheus
   |
   v
Grafana
```

---

# Features

* Monitor GitLab CI/CD pipelines
* Track branches and merge requests
* Collect metrics using Prometheus
* Visualize metrics using Grafana dashboards
* Custom Python exporter for branch metrics
* Containerized setup using Docker Compose

---

# Technologies Used

| Tool           | Purpose                    |
| -------------- | -------------------------- |
| Docker         | Containerization           |
| Docker Compose | Multi-container management |
| Prometheus     | Metrics collection         |
| Grafana        | Visualization & dashboards |
| Python         | Custom exporter            |
| GitLab API     | Fetch project information  |

---

# Project Structure

```text
Gitlab-monitoring/
│
├── Prometheus/
│   └── prometheus.yml
│
├── Dockerfile
├── docker-compose.yml
├── gcexporter.py
├── requirement.txt
└── gitlab-ci-pipelines-exporter.yml
```

---

# Services Overview

| Service                | Port | Description             |
| ---------------------- | ---- | ----------------------- |
| Grafana                | 3000 | Dashboard visualization |
| Prometheus             | 9090 | Metrics collection      |
| GitLab Exporter        | 8080 | GitLab pipeline metrics |
| Custom Python Exporter | 8500 | Branch count metrics    |

---

# Setup Instructions

## 1) Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/monitoring_gitlab_pipeline.git
cd monitoring_gitlab_pipeline
```

---

## 2) Install Docker & Docker Compose

### Ubuntu

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
```

---

## 3) Create GitLab Access Token

Go to:

```text
GitLab → Preferences → Access Tokens
```

Required scope:

```text
read_api
```

---

## 4) Configure GitLab Exporter

Edit:

```text
gitlab-ci-pipelines-exporter.yml
```

Replace:

```yaml
token: '<gitlab_token>'
```

With your real GitLab token.

Also update:

```yaml
projects:
  - name: group/project
```

---

## 5) Configure Python Exporter

Edit:

```text
gcexporter.py
```

Update:

```python
group_name='your-group'
auth_token='your-token'
project_id=123456
```

---

## 6) Build Containers

```bash
docker-compose build --no-cache
```

---

## 7) Start Services

```bash
docker-compose up -d
```

---

## 8) Verify Running Containers

```bash
docker ps -a
```

---

# Access Services

| Service                 | URL                                |
| ----------------------- | ---------------------------------- |
| Grafana                 | http://YOUR_SERVER_IP:3000         |
| Prometheus              | http://YOUR_SERVER_IP:9090         |
| GitLab Exporter Metrics | http://YOUR_SERVER_IP:8080/metrics |
| Python Exporter Metrics | http://YOUR_SERVER_IP:8500/metrics |

---

# Example Metric

```text
gitlab_branch_count 5
```

---

# Prometheus Scrape Configuration

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: monitoring
    static_configs:
      - targets: ['SERVER_IP:8080']

  - job_name: monitoring_manual
    static_configs:
      - targets: ['SERVER_IP:8500']
```

---

# Docker Compose Overview

The `docker-compose.yml` file manages:

* Grafana container
* Prometheus container
* GitLab exporter container
* Custom Python exporter container

It also handles:

* Port mapping
* Networking
* Volumes
* Environment variables

---

# Troubleshooting

## Exporter DOWN in Prometheus

Check container logs:

```bash
docker logs <container_name>
```

---

## Python Compatibility Issues

Use stable Python versions such as:

```dockerfile
FROM python:3.11
```

---

## Connection Refused

Verify containers are running:

```bash
docker ps -a
```

---

# Learning Outcomes

This project helps understand:

* Monitoring architecture
* Prometheus exporters
* Docker networking
* Docker Compose
* GitLab API integration
* Grafana dashboards
* Custom metrics
* DevOps observability concepts

---


# Author

Alaa Ibrahim

DevOps & MLOps Engineer
