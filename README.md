
# 🧠 AI Mesh Orchestrator

*A Distributed, Auto-Scaling AI Task Processing Framework*

---

## 🚀 Project Overview

**AI Mesh Orchestrator** is a **distributed micro-task orchestration system** designed to process heterogeneous AI workloads (text + image) with:

✅ Dynamic worker auto-scaling
✅ Fault-tolerant execution
✅ Smart task complexity detection
✅ Multi-queue workload isolation
✅ Worker health monitoring

The system mimics **production-grade distributed processing architectures** used in modern AI infrastructure.

---

## 🎯 Why This Project Exists

Real-world AI systems rarely fail because of models.

They fail because of:

* Unpredictable workload spikes
* Inefficient resource utilization
* Worker crashes / timeouts
* Queue bottlenecks
* Poor observability

This project focuses on solving the **systems engineering challenges behind AI**, not just inference.

---

## ⚙️ Core Capabilities

### ✅ Multi-Queue Task Architecture

Workloads are isolated by type:

* `text_queue` → NLP / Transformer tasks
* `image_queue` → Computer vision tasks

**Why this matters:**

Heavy image jobs cannot block lightweight text jobs — ensuring predictable latency.

---

### ✅ Task Complexity Detection

Each task is analyzed before queueing:

* Text → word count
* Image → resolution / size

Tasks are tagged:

* `small` (lightweight)
* `large` (computationally expensive)

**Why this matters:**

Scaling decisions are based on **workload weight**, not just task count.

---

### ✅ Dynamic Auto-Scaling Engine

Workers scale automatically:

* Minimum → 1 worker
* Maximum → 8 workers per queue

Scaling signals:

* Queue backlog
* Task complexity weights
* Idle cycles
* Cooldown windows

**Why this matters:**

Optimizes throughput **without wasting compute resources**.

---

### ✅ Fault-Tolerant Processing

The framework guarantees resilient execution via:

* Retry logic
* Task timeouts
* Dead-letter queues (DLQ)
* Redis metadata tracking

No silent failures. No lost tasks.

---

### ✅ Worker Health Monitoring

Each worker publishes heartbeats:

* `last_seen` timestamp
* Current load
* Worker status

Expired heartbeat = offline worker detection.

**Why this matters:**

Enables self-healing and scaling decisions.

---

## 🏗️ High-Level Architecture

```
Client → FastAPI API → Redis Queues → Workers → Redis Result Store
```

Components:

* **FastAPI** → Task submission & monitoring
* **Redis** → Broker + state store
* **Workers** → Task execution engine
* **Auto-Scaler** → Adaptive worker controller

---

## 🧰 Tech Stack

| Layer             | Technology               |
| ----------------- | ------------------------ |
| API Layer         | FastAPI                  |
| Queue / Broker    | Redis                    |
| AI Processing     | Transformers + OpenCV    |
| Containerization  | Docker / Docker Compose  |
| Scaling Logic     | Python-based Auto-Scaler |
| Concurrency Model | Blocking Queue (BRPOP)   |

---

## 🧠 Engineering Concepts Demonstrated

This project intentionally explores **distributed systems design patterns**:

✔ Workload isolation
✔ Elastic scaling
✔ Backpressure control
✔ Failure recovery
✔ Idempotent task tracking
✔ Health probing / heartbeat monitoring
✔ Decentralized pull-based scheduling

---

## 💥 What Makes This Project Interesting

Unlike typical task queues:

* Scaling is **complexity-aware**, not count-based
* Workers are **dynamically provisioned**, not static
* Queues are **typed & isolated**
* Reliability mechanisms are explicitly engineered
* System behavior is fully observable via Redis state

This resembles patterns seen in:

* Celery internals
* Kubernetes job controllers
* Cloud auto-scaling systems
* High-throughput async pipelines

---

## 🚀 Example Use Cases

* AI inference pipelines
* Batch LLM processing
* Image / video processing farms
* Background job systems
* Event-driven microservices
* Edge AI task distribution

---

## ▶️ Running the System

```bash
docker-compose up --build
```

Scaling workers dynamically:

```bash
docker-compose up --scale image_worker=4 --scale text_worker=2 -d
```

---

## 📊 Observability & Monitoring

System state is visible via Redis:

* Task lifecycle
* Queue depth
* Worker health
* Retry / failure states

Optional dashboard & metrics can be added via:

* Prometheus
* Grafana
* FastAPI WebSockets UI

---

## 🧩 Future Enhancements

Planned advanced features:

* Priority queues
* Distributed locking (RedLock)
* Kubernetes + KEDA scaling
* ML-driven scheduling
* Task cancellation / preemption
* Gossip-based worker coordination

---

# 👨‍💻 About the Author

I built this project to explore **distributed systems, fault tolerance, and adaptive infrastructure design** rather than just AI model usage.

My focus areas include:

* Distributed system behavior
* Performance & scaling logic
* Reliability engineering
* Queue-based architectures
* Containerized compute systems

I enjoy designing systems that remain **stable under load, resilient under failure, and efficient under constraints**.

---

# ⭐ Key Takeaway

This is not just a task queue.

It is a **self-adaptive distributed execution framework** designed to mimic real production system challenges.

---

---
