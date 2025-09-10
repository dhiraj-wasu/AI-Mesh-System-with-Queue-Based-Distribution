AI Mesh: Distributed Task Processing with FastAPI + Redis

A fault-tolerant, auto-scaling, AI-powered task orchestration system — built with FastAPI, Redis, Docker, and AI workers.
Handles text and image tasks with retries, timeouts, and dynamic scaling, inspired by production-grade MLOps pipelines.

Features

1.Redis-backed Queues for reliable task distribution (text_queue, image_queue)

2.Multi-worker Architecture (text & image workers run independently)

3.Fault Tolerance with retries (3x), timeouts, and dead-letter queue

4.Worker Health Monitoring via heartbeat + Redis TTL

5.Auto-scaling with load-aware worker scaling (Docker Compose/K8s)

6.Task Complexity Tagging (small vs large) for smarter scaling

7.Result Tracking with Redis hashes (status, retries, timestamps, result)

8.Dockerized for easy deployment & scaling across environments

Tech Stack

FastAPI → REST API for task submission & status

Redis → Queue + task store + worker monitoring

Docker Compose → Spin up API + Redis + workers

Transformers (Hugging Face) → Text sentiment analysis

OpenCV → Image face detection

Python Threading → Concurrent workers per container

📂 Project Structure
ai-mesh/
│── app/
│   ├── main.py           # FastAPI API endpoints
│   ├── redis_queue.py    # Redis connection
│   ├── enqueue.py        # Task enqueue logic + complexity tagging
│── workers/
│   ├── text_worker.py    # Processes text tasks
│   ├── image_worker.py   # Processes image tasks
│── scaler/
│   ├── auto_scale.py     # Dynamic worker scaling logic
│── docker-compose.yml    # Multi-container setup
│── Dockerfile            # Base image
│── README.md             # This file 🚀

Getting Started
1. Clone the repo
git clone https://github.com/yourusername/ai-mesh.git
cd ai-mesh

2. Start with Docker Compose
docker-compose up --build


This starts:

FastAPI API (on port 8000)

Redis (as queue broker)

Workers (text + image processors)

3. Submit a Task
curl -X POST "http://localhost:8000/submit" \
     -H "Content-Type: application/json" \
     -d '{"type": "text", "data": "I love this project!"}'


Response:

{"task_id": "123e4567-e89b-12d3-a456-426614174000"}

4. Check Task Status
curl "http://localhost:8000/status/123e4567-e89b-12d3-a456-426614174000"


Example response:

{
  "status": "done",
  "result": {"label": "POSITIVE", "score": 0.99}
}

Auto-Scaling Logic

Every 10s, scaler checks queue length & task complexity

Dynamically scales workers between 1 → 8

Large tasks weigh more → trigger faster scaling

Idle workers are scaled down after 3 empty cycles

Example Workflows

✅ Text Analysis → Sentiment analysis using Hugging Face Transformers
✅ Image Processing → Face detection using OpenCV
✅ Fault Tolerance → Retries up to 3x, then sent to dead-letter queue
✅ Auto-Scaling → Spin up more workers if queues get heavy

 Roadmap

 Add Prometheus + Grafana monitoring

 Support priority queues (high, medium, low)

 Add more AI models (summarization, OCR, speech-to-text)

 Implement DAG task dependencies

 Deploy on Kubernetes with HPA

Use Cases

AI Inference Gateway – Centralized API for ML models

🖼️ Batch Media Processing – Scale image/video processing pipelines

📄 NLP Workflows – Text classification, sentiment, summarization

🧑‍🤝‍🧑 Multi-tenant SaaS – Queue isolation per client with quotas

🏆 Why "AI Mesh"?

Because it’s like a mesh of AI workers dynamically scaling, self-healing, and collaborating to process tasks in real-time — just like production AI systems.
