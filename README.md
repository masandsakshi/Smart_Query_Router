# SmartQueryRouter: An Adaptive, Resource-Aware Database Proxy

SmartQueryRouter is a standalone, intelligent middleware layer built in Go. It acts as a smart proxy for distributed databases, routing queries to the best-performing backend node based on a combination of real-time health checks, historical performance data, and a latency-driven feedback loop.

---

### 🤔 The Problem
In a distributed database cluster, simply distributing load via round-robin is not enough. Nodes can become slow or unresponsive due to high CPU load, disk I/O bottlenecks, or network issues. A traditional proxy is blind to this degradation, continuing to send queries to failing nodes, which results in high latency and errors for the client.

### 💡 The Solution: SmartQueryRouter
SmartQueryRouter solves this by being **resource-aware and adaptive**. It constantly monitors the state of the cluster and uses that data to make intelligent routing decisions, ensuring queries are always sent to the healthiest and fastest available node.

---

### ✨ Key Features (Current Implementation)

*   **High-Performance Go Proxy:** A lightweight, concurrent core engine that adds minimal overhead to requests.
*   **Real-Time Health Checking:** Actively monitors all backend nodes via periodic TCP probes. Unhealthy nodes are automatically and temporarily removed from the routing pool.
*   **Adaptive Latency-Based Routing:** Moves beyond simple round-robin. It measures the latency of every query and maintains a moving average for each node. New requests are always sent to the healthy node with the lowest historical latency.
*   **Resilient Failover & Retry:** If a query to a chosen node fails unexpectedly, the proxy automatically retries the request on the next-best candidate, ensuring high availability.
*   **Full Observability Stack:** Exposes detailed performance metrics (node health, latency histograms, proxied request counts) via a `/metrics` endpoint, ready to be scraped by **Prometheus** and visualized in **Grafana**.

---

### 🗺️ Roadmap: Future Work

1.  **🧠 Predictive Routing with Machine Learning:**
    *   Implement a new, pluggable routing policy that uses a simple ML model (e.g., time-series forecasting) to *predict* node latency based on recent trends. This will allow the router to be proactive, avoiding nodes *before* they become critically slow.

2.  **🔌 Pluggable Database Adapters:**
    *   Build out the `adapters` for real-world databases like PostgreSQL and MongoDB that use binary TCP protocols instead of HTTP. This will make the router truly database-agnostic.

3.  **🐳 Full Dockerization:**
    *   Create a complete `docker-compose.yaml` file to run the entire stack (Router, Prometheus, Grafana, and mock backends) with a single `docker-compose up` command, making setup and testing effortless.

---

### 🛠️ Technology Stack
*   **Core:** Go (Golang)
*   **Observability:** Prometheus, Grafana
*   **Configuration:** YAML
*   **Protocols:** HTTP, TCP/IP
*   **Logging:** Zap (Structured Logging)

---

### 🤝 Contributing
This is a personal learning project, but contributions, ideas, and feedback are welcome. Please feel free to open an issue or submit a pull request.
