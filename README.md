# Kafka Grafana Dashboards

Collection of Grafana dashboards for monitoring **Apache Kafka components** with Prometheus exporters.  
Designed and tested with **KRaft mode clusters** (no ZooKeeper).

## 📂 Available Dashboards

### 1. Kafka Broker Overview (`kafka-broker-overview.json`)

Comprehensive Grafana dashboard for monitoring **Kafka brokers**.  
Tracks JVM memory & GC, request handlers, network processors, throughput, replication traffic, request/response latencies (p95/p999), under-replicated partitions, disk I/O, and overall broker health using Prometheus.

#### ✅ Requirements

- **Grafana:** 11.4+
- **Data source:** Prometheus
- **Exporters:**
  - Kafka JMX Exporter (`:8080`)
  - Kafka Controller JMX Exporter (`:8079`)
  - Node Exporter (`:9100`)

> 📝 This dashboard is designed and tested with **Apache Kafka in KRaft mode**.

#### 🔌 Prometheus Scrape Config

```yaml
- job_name: kafka-broker-jmx
  static_configs:
    - targets: ["localhost:8080"]

- job_name: kafka-controller-jmx
  static_configs:
    - targets: ["localhost:8079"]

- job_name: node-exporter
  static_configs:
    - targets: ["localhost:9100"]
```

## 🧩 Variables

- `$cluster` — Kafka cluster label
- `$environment` — Environment (e.g., prod, staging)

> Prometheus metrics are filtered using labels `_cluster="$cluster"` and `_environment="$environment"`.

## 🔧 How to use

1. Import the JSON dashboard into Grafana.
2. Select your **Prometheus** data source.
3. Map variables (`$cluster`, `$environment`) to your metric labels.
4. Verify that Prometheus is scraping the exporters at `:8080`, `:8079`, and `:9100`.
