# 🐧 Linux System Monitoring Stack

A comprehensive monitoring solution for Linux systems with hardware health monitoring, container metrics, and system performance tracking.

## 🛠️ Configuration
### Environment Variables
Create `.env` (example `.env.template `file) file with your configuration:
```ini
# VictoriaMetrics configuration
VM_REMOTE_WRITE_URL=http://<HOST>:8427/insert/0/prometheus/api/v1/write
VM_REMOTE_WRITE_USERNAME=<VM_REMOTE_WRITE_USERNAME>
VM_REMOTE_WRITE_PASSWORD=<VM_REMOTE_WRITE_PASSWORD>

# Exporters configuration
NODE_EXPORTER_PORT=9110
...
```

## 🚀 Quick Start

```bash
docker compose -f composes/docker-compose-vm.yml \
               -f composes/docker-compose-devices-monitoring.yml \
               -f composes/docker-compose-monitoring.yml \
               --env-file .env up -d
```

## 📊 Monitoring Architecture
```text
┌─────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│   Exporters     │───▶ │    vmagent       │───▶ │  VictoriaMetrics │
│  (Metrics)      │     │  (Collection)    │     │   (Storage)      │
└─────────────────┘     └──────────────────┘     └──────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                         ┌───────▼───────┐
                         │   Grafana     │
                         │(Visualization)│
                         └───────────────┘
```

## 🔧 Components
### 📡 Metrics Collection
`vmagent` - **Metrics Collector**
- **Endpoint**: http://localhost:8429

- **Description**: Lightweight metrics collector that scrapes, filters, and forwards metrics to VictoriaMetrics

- **Features**:

  - Service discovery

  - Relabeling

  - Data filtering

  - Remote write capabilities

### 🐳 Container Monitoring
`cAdvisor` - **Container Metrics**

- **Endpoint**: http://localhost:8081

- **Metrics**: CPU, memory, filesystem, and network usage for containers

- **Features**:

  - Container resource isolation metrics

  - Historical resource usage

  - Container performance analysis

`Docker State Exporter `- **Container State**

- **Endpoint**: http://localhost:8082

- **Metrics**: Container states, image versions, restart counts

- **Features**:

  - Container health status

  - Image version tracking

  - Restart history monitoring

`Node Exporter` - **System Metrics**
- **Endpoint**: http://localhost:9110

- **Metrics**: Hardware and OS metrics from *NIX kernels

- **Coverage**:

  - CPU usage and load

  - Memory utilization

  - Disk I/O and space

  - Network statistics

  - System load and uptime

### 💾 Hardware Health Monitoring
`smartctl Exporter` - **Disk Health**
- **Endpoint**: http://localhost:9633

- **Dependencies**:
    ```bash
    sudo apt-get install smartmontools
    ```
- **Metrics**: S.M.A.R.T. attributes for HDD/SSD health monitoring

- **Coverage**:

  - Disk temperature

  - Bad sectors count

  - Read/Write error rates

  - SSD wear leveling

  - Power-on hours and cycles

## 📈 Key Metrics Monitored
### 🔴 Critical Alerts
- **Disk Failure Prediction**: Reallocated sectors, pending sectors, uncorrectable errors

- **SSD End-of-Life**: Remaining lifespan below 10%

- **High Temperature**: Disks exceeding safe operating temperatures

- **Container Health**: Frequent restarts, resource exhaustion

### 🟡 Performance Metrics
- **System**: CPU load, memory pressure, disk I/O latency

- **Storage**: Disk utilization, read/write throughput, queue depth

- **Containers**: Resource limits, memory usage, network bandwidth

### 🟢 Health Indicators
- **Hardware**: Power-on time, load cycles, interface errors

- **System**: Uptime, service availability, update status

## 📊 Dashboard Features
### 🎯 S.M.A.R.T. Disk Health Dashboard
- Real-time disk temperature monitoring

- Critical attribute tracking (reallocated sectors, pending sectors)

- SSD lifespan prediction

- Historical trend analysis

- Multi-disk comparison views

### 🐳 Container Performance Dashboard
- Resource utilization per container

- Memory and CPU limits tracking

- Network I/O monitoring

- Storage usage analytics

### 🖥️ System Overview Dashboard
- Host-level resource monitoring

- Hardware health status

- Service availability

- Performance trending

## 🔗 Useful Links

### Core Components
- **vmagent**: [Documentation](https://docs.victoriametrics.com/victoriametrics/vmagent) | [Source](https://github.com/VictoriaMetrics/VictoriaMetrics)

- **VictoriaMetrics**: [Documentation](https://docs.victoriametrics.com/) | [Source](https://github.com/VictoriaMetrics/VictoriaMetrics)

### Exporters
- **cAdvisor**: [Documentation](https://github.com/google/cadvisor) | [Source](https://github.com/google/cadvisor)

- **Docker State Exporter**: [Documentation](https://github.com/karugaru/docker_state_exporter) | [Source](https://github.com/karugaru/docker_state_exporter)

- **Node Exporter**: [Documentation](https://github.com/prometheus/node_exporter) | [Source](https://github.com/prometheus/node_exporter)

- **smartctl Exporter**: [Documentation](https://github.com/prometheus-community/smartctl_exporter) | [Source](https://github.com/prometheus-community/smartctl_exporter)

### Additional Resources
- **Prometheus Querying**: [PromQL Guide](https://prometheus.io/docs/prometheus/latest/querying/basics/)

- **Grafana Dashboards**: [Dashboard Examples](https://grafana.com/grafana/dashboards/)

- **S.M.A.R.T. Attributes**: [Attribute Reference](https://en.wikipedia.org/wiki/S.M.A.R.T.#Known_ATA_S.M.A.R.T._attributes)
