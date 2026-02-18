

# **AI Mesh: Distributed Task Processing with FastAPI + Redis**

A fault-tolerant, auto-scaling, AI-powered task orchestration system built with **FastAPI**, **Redis**, **Docker**, and AI workers.

Inspired by production-grade **MLOps pipelines**, this system handles text and image tasks with retries, timeouts, worker health monitoring, and dynamic scaling.

---

## 🚀 Features

* **Redis-backed Queues** for reliable task distribution (`text_queue`, `image_queue`)
* **Multi-worker Architecture** (text & image workers run independently)
* **Fault Tolerance** with retries (3×), timeouts, and dead-letter queue
* **Worker Health Monitoring** via heartbeat + Redis TTL
* **Auto-scaling** with load-aware worker scaling
* **Task Complexity Tagging** (small vs large) for smarter scaling
* **Result Tracking** with Redis hashes (status, retries, timestamps, result)
* **Dockerized Deployment** for easy scaling across environments

---

## 🧱 Tech Stack

* **FastAPI** → REST API for task submission & status
* **Redis** → Queue broker + task store + worker monitoring
* **Docker Compose** → Multi-container orchestration
* **Transformers (Hugging Face)** → Text sentiment analysis
* **OpenCV** → Image face detection
* **Python Threading** → Concurrent workers per container

---

## 📂 Project Structure

```
ai-mesh/
│── app/
│   ├── main.py          # FastAPI API endpoints
│   ├── redis_queue.py   # Redis connection
│   ├── enqueue.py       # Task enqueue logic + complexity tagging
│
│── workers/
│   ├── text_worker.py   # Processes text tasks
│   ├── image_worker.py  # Processes image tasks
│
│── scaler/
│   ├── auto_scale.py    # Dynamic worker scaling logic
│
│── docker-compose.yml   # Multi-container setup
│── Dockerfile           # Base image
│── README.md            # Documentation
```

---

## ⚡ Getting Started

### Clone the Repository

```bash
git clone https://github.com/yourusername/ai-mesh.git
cd ai-mesh
```

### Start the System

```bash
docker-compose up --build
```

This starts:

* FastAPI API (port **8000**)
* Redis (queue broker)
* Workers (text + image processors)

---

## 📬 Submit a Task

```bash
curl -X POST "http://localhost:8000/submit" \
-H "Content-Type: application/json" \
-d '{"type": "text", "data": "I love this project!"}'
```

**Response**

```json
{"task_id": "123e4567-e89b-12d3-a456-426614174000"}
```

---

## 🔎 Check Task Status

```bash
curl "http://localhost:8000/status/123e4567-e89b-12d3-a456-426614174000"
```

**Example Response**

```json
{
  "status": "done",
  "result": {"label": "POSITIVE", "score": 0.99}
}
```

---

## 📈 Auto-Scaling Logic

Every **10 seconds**, the scaler:

* Checks queue length & task complexity
* Dynamically scales workers between **1 → 8**
* Large tasks weigh more → trigger faster scaling
* Idle workers scale down after **3 empty cycles**

---

## ✅ Example Workflows

* **Text Analysis** → Sentiment analysis using Hugging Face Transformers
* **Image Processing** → Face detection using OpenCV
* **Fault Tolerance** → Retries up to 3× → Dead-letter queue fallback
* **Auto-Scaling** → Workers scale based on system load

---

## 🛣️ Roadmap

* Add Prometheus + Grafana monitoring
* Support priority queues (high / medium / low)
* Add more AI models (summarization, OCR, speech-to-text)
* Implement DAG task dependencies
* Deploy on Kubernetes with HPA

---

## 💡 Use Cases

* **AI Inference Gateway** – Centralized API for ML models
* **Batch Media Processing** – Scalable image/video pipelines
* **NLP Workflows** – Classification, sentiment, summarization
* **Multi-tenant SaaS** – Queue isolation & quotas

---

## 🏆 Why *"AI Mesh"*?

Because it behaves like a mesh of AI workers — dynamically scaling, self-healing, and collaboratively processing tasks in real time — similar to real-world production AI systems.

---

