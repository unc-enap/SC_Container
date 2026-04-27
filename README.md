# SC_Container
Grafana and InfluxDB Container used for SC server at UNC 
InfluxDB 3.0 & Grafana Stack
This repository contains a docker-compose.yml file to deploy a containerized monitoring stack using InfluxDB 3 Core and Grafana.

Running these services in Docker containers ensures consistent environments and prevents future versioning conflicts.

Prerequisites
Docker and Docker Compose installed on the host machine.
The host machine must have the following directories created for persistent data storage:
/Volumes/data/InFluxDB_data
/Volumes/data/Grafana_data (Note: Ensure the Docker daemon has read/write permissions for these directories).
Quick Start
Clone or download this repository to your host machine.
Open a terminal and navigate to the directory containing the docker-compose.yml file.
Start the stack in detached mode:
bash

Copy code
docker compose up -d

To stop the stack:
bash

Copy code
docker compose down

Accessing the Services
Grafana
URL: http://<host-ip>:3000 (e.g., http://localhost:3000 or http://152.19.204.153:3000)
Default Username: admin
Default Password: admin (You will be prompted to change this on your first login).
InfluxDB 3 Core
URL: http://<host-ip>:80
API Token: apiv3_ITYA3olmUbFbDytHAjgArTvr4dqteH5DtHVvJe0fPoB8Zg1iU6YdE7aN16Wc3h9KHzZWNeqbp1fkNyC0sIEspQ
Architecture & Configuration Details
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
⚠️ Deployment Notes & Recommendations
Grafana Password: Your docker-compose.yml sets the default Grafana password to admin. However, in your previous announcement, you told users the password was sc_grafana. You can either:
Change GF_SECURITY_ADMIN_PASSWORD: admin to GF_SECURITY_ADMIN_PASSWORD: sc_grafana in the compose file before running it.
Or, log in manually the first time with admin and change it to sc_grafana in the Grafana UI.
Host Paths: The volume paths (/Volumes/data/...) are formatted for macOS. If the new ENAP_SC machine is a Linux server, you may want to update these paths to standard Linux directories (e.g., /opt/data/InFluxDB_data or ./data/influxdb).
Port 80: InfluxDB is mapped to port 80 on the host. On Linux systems, binding to ports below 1024 usually requires root/sudo privileges.
Security: The InfluxDB API token is hardcoded in the compose file. Ensure this file is kept secure and not exposed publicly.








