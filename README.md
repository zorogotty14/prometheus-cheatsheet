# Prometheus Cheatsheet

## **Prometheus Overview**
Prometheus is an open-source monitoring and alerting toolkit for collecting and querying time-series metrics.

---

## **Prometheus Setup**
```sh
prometheus --version             # Check Prometheus version
prometheus --config.file=<path>  # Start Prometheus with a specific config file
```

---

## **Basic Prometheus Configuration (`prometheus.yml`)**
```yaml
global:
  scrape_interval: 15s  # How often to scrape targets by default
  evaluation_interval: 15s # How often to evaluate rules

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
```

---

## **Querying Metrics using PromQL**
```sh
up                                  # Check if targets are up
rate(http_requests_total[5m])       # Requests per second over 5 minutes
sum by(instance) (node_cpu_seconds_total)  # Total CPU seconds by instance
avg_over_time(node_memory_used_bytes[10m])  # Average memory usage over 10 minutes
```

---

## **Recording Rules (Aggregation and Precomputing Metrics)**
```yaml
groups:
  - name: example_rules
    interval: 30s
    rules:
      - record: job:http_requests:rate5m
        expr: rate(http_requests_total[5m])
```

---

## **Alerting with Prometheus Alertmanager**
```yaml
route:
  receiver: 'default'
  group_wait: 10s
  group_interval: 5m
  repeat_interval: 3h
receivers:
  - name: 'default'
    email_configs:
      - to: 'alerts@example.com'
```

---

## **Useful Prometheus Commands**
```sh
curl http://localhost:9090/api/v1/targets  # Check active targets
curl http://localhost:9090/api/v1/alerts   # Check active alerts
```

---

## **Useful Prometheus Resources**
- [Prometheus Docs](https://prometheus.io/docs/)
- [PromQL Cheat Sheet](https://promlabs.com/promql-cheat-sheet/)
- [Prometheus GitHub](https://github.com/prometheus/prometheus)

---

This cheatsheet provides a quick reference for Prometheus setup, querying, and alerting. Let me know if you need more details!

