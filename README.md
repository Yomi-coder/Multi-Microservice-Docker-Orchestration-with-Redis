# Multi-Microservice Docker Orchestration with Redis

A containerized microservice architecture demonstrating service communication and orchestration using Docker Compose. This project features an API service built with Flask that tracks page visit counts and a Worker service that monitors system status, both communicating through a shared Redis cache.

## 🎯 Project Overview

This project is designed to teach fundamental DevOps and microservice architecture concepts including:
- **Multi-Service Architecture**: Building and managing multiple independent microservices
- **Container Orchestration**: Using Docker Compose to manage containerized services
- **Inter-Service Communication**: Redis-based message passing and caching
- **Containerization**: Dockerizing Python applications

## 🏗️ Architecture

```
User Request
    ↓
API Service (Flask) ←→ Redis Cache ←→ Worker Service
    ↓
Response with Visit Count
```

### Services

1. **API Service** - Flask REST API
   - Serves HTTP requests on port 5000
   - Tracks page visit counts in Redis
   - Endpoint: `GET /`

2. **Worker Service** - Background Worker
   - Monitors and updates status every 5 seconds
   - Communicates with Redis cache
   - Runs continuously in background

3. **Redis Cache** - In-memory Data Store
   - Shared communication layer between services
   - Caches visit counts and worker status
   - Port: 6379

## 📋 Tech Stack

- **Backend**: Python
- **Web Framework**: Flask
- **Caching/Messaging**: Redis
- **Containerization**: Docker & Docker Compose
- **Orchestration**: Docker Compose

## 🚀 Quick Start

### Prerequisites

- Docker installed
- Docker Compose installed
- Windows PowerShell or any terminal

### Installation & Setup

1. **Clone the repository**
```bash
git clone <your-repo-url>
cd Project
```

2. **Build and Start Services**
```bash
# Build all services
docker-compose build

# Start all services in background
docker-compose up --build -d
```

3. **Verify Services Are Running**
```bash
docker-compose ps
```

## 📖 Usage

### Access the API
Open your browser or use curl to access the API:
```bash
curl http://localhost:5000/
```

**Expected Response:**
```
Hello! This page has been visited X times.
```

Each visit increments the counter stored in Redis.

### View Service Logs
```bash
# All services
docker-compose logs

# Specific service
docker-compose logs api
docker-compose logs worker
docker-compose logs redis
```

### Stop Services
```bash
docker-compose down
```

## 📂 Project Structure

```
Project/
├── docker-compose.yml      # Service orchestration configuration
├── api/
│   ├── app.py              # Flask API application
│   ├── dockerfile          # API service Docker image
│   └── requirements.txt     # Python dependencies
├── worker/
│   ├── worker.py           # Background worker script
│   └── dockerfile          # Worker service Docker image
└── README.md               # This file
```

## 📝 File Details

### app.py (API Service)
- Flask application that handles HTTP requests
- Increments a counter in Redis on each request
- Returns the current visit count

### worker.py (Worker Service)
- Continuous loop that runs every 5 seconds
- Updates worker status in Redis
- Demonstrates async operations

### docker-compose.yml
- Defines all three services (api, worker, redis)
- Configures networking between services
- Maps ports and environment variables
- Sets build contexts for custom Dockerfiles

## 📊 Expected Output

When you run `docker-compose logs`, you should see:

```
redis   | Ready to accept connections
api     | Running on http://0.0.0.0:5000
worker  | Worker is running...
worker  | Worker is running...   ← repeats every 5 seconds
```

## 🔧 Common Commands

| Command | Description |
|---------|-------------|
| `docker-compose up --build` | Build and start all services |
| `docker-compose up --build -d` | Start in background |
| `docker-compose ps` | List running services |
| `docker-compose logs` | View all service logs |
| `docker-compose logs -f api` | Follow API logs |
| `docker-compose down` | Stop and remove containers |
| `docker-compose exec api bash` | Access API container shell |

## 🎓 Learning Outcomes

By working with this project, you'll understand:

1. **Multi-Service Architecture**
   - How to split applications into independent services
   - Service responsibility separation

2. **Container Orchestration**
   - Docker Compose configuration and management
   - Service dependencies and networking

3. **Service Communication**
   - Redis as a communication medium
   - Data sharing between containers

4. **DevOps Fundamentals**
   - Containerization best practices
   - Environment configuration
   - Service health monitoring

## 🐛 Troubleshooting

### Services won't start
```bash
# Check for port conflicts
docker-compose ps

# View detailed error logs
docker-compose logs
```

### Redis connection error
- Ensure all services are on the same Docker network
- Check `docker-compose.yml` for correct service names

### Worker keeps restarting
- Check worker logs: `docker-compose logs worker`
- Verify Python syntax in `worker.py`

## 📚 Next Steps

1. Scale the worker service: `docker-compose up --scale worker=3`
2. Add a database service (PostgreSQL/MongoDB)
3. Implement health checks
4. Add load balancing with Nginx
5. Deploy to Kubernetes

## 📄 License

This project is open source and available for educational purposes.

## 👤 Author

DevOps Learning Project

---

**Happy Learning! 🚀**
