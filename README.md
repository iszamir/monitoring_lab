# Prometheus + Grafana Monitoring Lab

### **Folder Structure for Documentation**
monitoring-lab/
├── screenshots/
│ ├── prometheus-cpu-usage-query.png
│ ├── prometheus-disk-space-query.png
  ├── prometheus-memory-usage-query.png
│ └── grafana-dashboard-full.png
├── prometheus.yml      # Prometheus configuration
├── docker-compose.yml  # Container orchestration
└── README.md

## Steps
1.  **Launch Services**:
   docker-compose up -d

3. Verify Components:

Prometheus: http://<server-ip>:9090
Grafana: http://<server-ip>:3000 (admin/admin)
Node Exporter: http://<server-ip>:9100/metrics

3. Configure Grafana:

Add Prometheus data source (URL: http://prometheus:9090)
Import dashboard ID 1860 (Node Exporter Full)

## Sample Queries
promql
# Memory Usage
(node_memory_MemTotal_bytes - node_memory_MemFree_bytes) / node_memory_MemTotal_bytes * 100

# CPU Usage
100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100)

# Disk Space
100 - (node_filesystem_avail_bytes{mountpoint="/"} / node_filesystem_size_bytes{mountpoint="/"} * 100)

## Troubleshooting
No Data? Check targets at http://<ip>:9090/targets

Dashboard Issues? Verify data source in Grafana

Container Problems? Run:
bash
docker-compose logs -f

## Port Information
   | Service         | Port  |
   |-----------------|-------|
   | Prometheus      | 9090  |
   | Grafana         | 3000  |
   | Node Exporter   | 9100  |

## Health Check Command
curl -s http://localhost:9090/-/healthy && echo "Prometheus OK" || echo "Error"

## Cleanup instructions
docker-compose down -v  # Stops and removes containers


