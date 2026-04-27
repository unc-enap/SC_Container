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

   
   
