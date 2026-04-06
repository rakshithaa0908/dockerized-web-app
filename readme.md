# Dockerized Voting Web Application

This project demonstrates a multi-container voting web application built with Docker and Docker Compose. The app includes a frontend, backend, background workers, in-memory caching, and a database, all running in isolated containers connected through Docker networking.

---

## Concepts

### Technologies Used
- Docker
- Docker Compose
- Python (Flask) — Voting service
- Node.js — Result service
- C# (.NET) — Background worker
- Redis — In-memory cache / message broker
- PostgreSQL — Database

### Docker
Packages each service (vote, result, worker, Redis, PostgreSQL) into isolated containers that communicate through a shared Docker network.

### Docker Compose
Defines and manages all services in a single docker-compose.yaml file, enabling the entire application to start with one command.

---
## Prerequisites
- Docker installed on your machine
- Docker Compose installed
- Git & GitHub account

---

## Deployment Steps

For detailed deployment instructions, see [docs/deployment-steps.md](docs/deployment-steps.md)

---

## Project Structure
```
dockerized-web-app/
│
├── docs/
│   ├── deployment-steps.md
│   └── screenshots/
│       ├── vote.png
│       ├── result.png
│       └── architecture.png
├── result/
│   ├── static/
│   │   └── style.css
│   ├── Dockerfile
│   ├── app.js
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   ├── server.js
│   └── socket.io.js
├── vote/
│   ├── static/
│   │   └── style.css
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
├── worker/
│   ├── Dockerfile
│   ├── Program.cs
│   └── worker.csproj
├── docker-compose.yaml
├── README.md
├── .dockerignore
└── LICENSE
```

---

## Architecture Diagram
![Architecture](docs/screenshots/architecture.png)

---

## Screenshots

**Voting Application (Frontend)**  
![Voting](docs/screenshots/vote.png)

**Result (Live Results)**  
![Result](docs/screenshots/result.png)

---
## About This Project
Built to demonstrate multi-container application architecture using Docker and Docker Compose. Each service runs in an isolated container and communicates through Docker networking — simulating a real-world microservices setup.

---
## Limitations
- Requires Docker and Docker Compose installed locally
- No HTTPS/TLS configured — runs over HTTP only
- Data is lost when containers are stopped (no persistent volumes configured)
- Not intended for production use

---
## License

MIT License. See `LICENSE` file for details.

