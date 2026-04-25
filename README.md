# 🐧 Linux System Monitoring Stack

A comprehensive monitoring solution for Linux systems with hardware health monitoring, container metrics, and system performance tracking.

## 🛠️ Configuration
### Environment Variables
Create `.env` (example `.env.template `file) file with your configuration:

## 🚀 Quick Start

```bash

HOSTNAME=$(hostname) docker compose --env-file .env \
-f ./composes/docker-compose.yml \ 
-f ./composes/docker-compose-monitoring.yml \
-f ./composes/docker-compose-alloy.yml \
-f ./composes/docker-compose-devices-monitoring.yml \
-f ./composes/docker-compose-vmagent.yml \
up -d
```
