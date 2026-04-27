# InfluxDB 3.0 & Grafana Stack

This repository contains a `docker-compose.yml` file to deploy a containerized monitoring stack using **InfluxDB 3 Core** and **Grafana**. 

Running these services in Docker containers ensures consistent environments and prevents future versioning conflicts.

## Prerequisites

- **Docker** and **Docker Compose** installed on the host machine.
- The host machine must have the following directories created for persistent data storage:
  - `/Volumes/data/InFluxDB_data`
  - `/Volumes/data/Grafana_data`
  *(Note: Ensure the Docker daemon has read/write permissions for these directories).*

## Quick Start

1. Clone or download this repository to your host machine.
2. Open a terminal and navigate to the directory containing the `docker-compose.yml` file.
3. Start the stack in detached mode:
   ```bash
   docker compose up -d```

To stop the stack:
```bash
docker compose down
```

## Accessing the Services
### Grafana
URL: http://<host-ip>:3000 (http://localhost:3000-if using same machine)
InfluxDB 3 Core
URL: http://<host-ip>:80

### Architecture & Configuration Details
Both services run on a shared custom bridge network (influx-net) allowing them to communicate securely with each other.
1. InfluxDB (influxdb3-core)
Image: influxdb:3-core
Ports: Exposed on host port 80 (maps to container port 8181).
Storage: Data is persistently stored on the host at /Volumes/data/InFluxDB_data.
Configuration: Configured to use local file object storage (--object-store=file) and initialized with a predefined Operator/API token via environment variables.
2. Grafana (grafana)
Image: grafana/grafana:latest
Ports: Exposed on host port 3000.
Storage: Data (dashboards, users, data source configurations) is persistently stored on the host at /Volumes/data/Grafana_data.
Dependencies: Grafana is configured to wait for InfluxDB to start before initializing.


   
