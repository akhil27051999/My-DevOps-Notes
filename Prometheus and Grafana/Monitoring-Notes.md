# 📊 Prometheus

### 1. What is Prometheus?

Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. It is designed for reliability and scalability, focusing on time-series data collection and querying.

### 2. Prometheus Architecture

* **Prometheus Server**: Scrapes and stores time-series metrics.
* **Client Libraries**: Used to instrument application code.
* **Exporters**: Convert third-party metrics into Prometheus format.
* **Pushgateway**: For short-lived jobs to push metrics.
* **Alertmanager**: Manages alerts, deduplication, silencing, and notifications.
* **UI & API**: Built-in dashboard and REST API for queries.

### 3. Core Concepts

| Term            | Description                                                                              |
| --------------- | ---------------------------------------------------------------------------------------- |
| **Time Series** | Stream of timestamped values belonging to the same metric and label set.                 |
| **Metric**      | A numeric measurement with optional labels. E.g., `http_requests_total{method=\"GET\"}`. |
| **Labels**      | Key-value pairs that distinguish different series of the same metric.                    |
| **Scrape**      | Prometheus pulls metrics from targets at defined intervals.                              |
| **Target**      | A monitored endpoint that exposes metrics.                                               |
| **Job**         | A group of targets with similar functions (e.g., all Node Exporters).                    |
| **Instance**    | A single target (IP\:port).                                                              |

### 4. Data Model

Prometheus stores all data as **time series**:

* Identified by a **metric name** and set of **labels**.
* Each data point: `<timestamp, value>`

Example:

```
http_requests_total{method="GET", handler="/api"} => 7542 at 1620003000
```

### 5. Installation & Configuration

#### Manual Installation (Linux)

```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
tar -xvf prometheus-*.tar.gz
cd prometheus-*/
./prometheus --config.file=prometheus.yml
```

#### Docker

```bash
docker run -d \
  -p 9090:9090 \
  -v /path/to/prometheus.yml:/etc/prometheus/prometheus.yml \
  prom/prometheus
```

### 6. prometheus.yml - Key Sections

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['localhost:9100']
```

### 7. PromQL - Query Language

| PromQL                                                 | Description                                |
| ------------------------------------------------------ | ------------------------------------------ |
| `up`                                                   | Returns 1 if the target is up, 0 if down.  |
| `rate(http_requests_total[1m])`                        | Per-second average increase over 1 minute. |
| `avg by (job)(rate(cpu_seconds_total[5m]))`            | CPU usage per job.                         |
| `sum(rate(container_memory_usage_bytes[5m])) by (pod)` | Memory usage by pod.                       |

### 8. Exporters

Exporters expose metrics in Prometheus format:

| Exporter       | Port | Metrics             |
| -------------- | ---- | ------------------- |
| Node Exporter  | 9100 | OS/host metrics     |
| cAdvisor       | 8080 | Container metrics   |
| Blackbox       | 9115 | Probes for HTTP/TCP |
| MySQL Exporter | 9104 | MySQL metrics       |

### 9. Alerting with Alertmanager

* Prometheus sends alerts to Alertmanager.
* Alertmanager groups, deduplicates, and routes alerts.
* Supports email, Slack, PagerDuty, Webhooks.

#### Basic Alerting Rule

```yaml
alert: HighCPUUsage
expr: avg(rate(node_cpu_seconds_total[5m])) > 0.8
for: 2m
labels:
  severity: critical
annotations:
  summary: "High CPU usage detected"
```

#### alertmanager.yml Example (Slack Notification)

```yaml
global:
  resolve_timeout: 5m
  slack_api_url: 'https://hooks.slack.com/services/XXXX/XXXX/XXXX'

route:
  group_by: ['alertname']
  group_wait: 10s
  group_interval: 5m
  repeat_interval: 3h
  receiver: 'slack-notifications'

receivers:
  - name: 'slack-notifications'
    slack_configs:
      - channel: '#alerts'
        send_resolved: true
```

# 📈 Grafana

### 1. What is Grafana?

Grafana is an open-source analytics and monitoring platform. It connects to various data sources and helps visualize data in dashboards.

### 2. Grafana Core Features

* **Data Sources**: Prometheus, Loki, MySQL, Elasticsearch, etc.
* **Panels**: Graphs, heatmaps, tables, gauges.
* **Dashboards**: Collections of panels for a service/system.
* **Templating**: Variables to create dynamic dashboards.
* **Alerting**: Alerts on thresholds with notifications.
* **Annotations**: Visual markers for events.

### 3. Installation

#### Ubuntu/Debian

```bash
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
sudo apt-get update
sudo apt-get install grafana
sudo systemctl start grafana-server
```

#### Docker

```bash
docker run -d -p 3000:3000 grafana/grafana
```

Default credentials: `admin / admin`

### 4. Connect Grafana to Prometheus

1. Go to **Configuration > Data Sources**
2. Click **Add data source**, select **Prometheus**
3. Enter `http://localhost:9090`, click \*\*Save & Test\`

### 5. Dashboard Basics

* Each **dashboard** can have multiple **rows** and **panels**.
* Use **query editor** with PromQL.
* Apply **templating variables** for reusable dashboards.
* Share dashboards using JSON export/import.

### 6. Alerting in Grafana

* Configure thresholds in panels.
* Add alert rules: evaluation interval, condition.
* Define **notification channels** (Slack, Email).

### 7. Common Use Cases

* Infrastructure metrics (Node Exporter, Kube-state).
* Application metrics (custom instrumentation).
* Alerting on service health.
* Visualizing Kubernetes cluster state.


# 🛠️ Real-time Troubleshooting

### Prometheus Issues

| Problem          | Cause                              | Fix                                                                       |
| ---------------- | ---------------------------------- | ------------------------------------------------------------------------- |
| Target Down      | Wrong IP/port or app crashed       | Validate IP and port, app logs                                            |
| Slow Queries     | Too many time series or long-range | Use `rate`, `irate`, avoid high cardinality                               |
| Prometheus Crash | OOM or corrupted TSDB              | Use memory limits, restart with `--storage.tsdb.allow-overlapping-blocks` |

### Grafana Issues

| Problem            | Cause                   | Fix                                  |
| ------------------ | ----------------------- | ------------------------------------ |
| "No Data"          | Bad query or time range | Validate PromQL and panel time       |
| Data source error  | Wrong URL               | Use `curl <URL>` to check connection |
| Dashboard slowness | Too many queries/panels | Use intervals, query optimization    |


## 🔐 Best Practices

### Prometheus

* Don't expose Prometheus UI publicly.
* Avoid dynamic labels (UUID, IP).
* Aggregate early with recording rules.
* Use relabeling to filter targets.

### Grafana

* Use folders to organize dashboards.
* Version control dashboards via JSON.
* Backup dashboards regularly.
* Configure access control (Viewer, Editor, Admin).


## 📚 End-to-End Monitoring Setup for Microservices

### Scenario: Monitor a 3-tier microservices app (frontend, backend, database)

#### Tools:

* **Prometheus**: Metrics scraping
* **Node Exporter**: OS metrics from all services
* **Custom metrics**: Via Prometheus client libraries (Python, Go, Java)
* **Grafana**: Visualization
* **Alertmanager**: Notification handling

#### Setup Steps:

1. **Instrument code** using Prometheus libraries:

   * `prometheus_client` for Python
   * `prometheus-client` for Java
2. **Expose /metrics endpoint** from each service.
3. **Deploy Node Exporter** on each node.
4. **Configure Prometheus**:

   ```yaml
   scrape_configs:
     - job_name: 'frontend'
       static_configs:
         - targets: ['frontend-svc:8000']
     - job_name: 'backend'
       static_configs:
         - targets: ['backend-svc:9000']
     - job_name: 'database'
       static_configs:
         - targets: ['db-svc:9104']
   ```
5. **Deploy Alertmanager** and configure routes.
6. **Create dashboards in Grafana**:

   * Latency panels using `rate(http_request_duration_seconds_sum[1m]) / rate(http_request_duration_seconds_count[1m])`
   * Error rate panels using `rate(http_requests_total{status=~"5.."}[5m])`
   * DB metrics like QPS, connections
7. **Define alerts**:

   * CPU > 80%
   * Request latency > 2s
   * Error rate > 5%
8. **Integrate Slack/Email** in Alertmanager.

## 📚 References

* Prometheus Docs: [https://prometheus.io/docs](https://prometheus.io/docs)
* Grafana Docs: [https://grafana.com/docs](https://grafana.com/docs)
* PromQL Cheatsheet: [https://promlabs.com/promql-cheat-sheet](https://promlabs.com/promql-cheat-sheet)
* Grafana Dashboards: [https://grafana.com/grafana/dashboards](https://grafana.com/grafana/dashboards)

