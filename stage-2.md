# 📦 DevOps Roadmap – Stage 2: Containers & Docker

Containers solve the problem of "it works on my machine" by packaging code, dependencies, and environment together. Docker is the most widely used container platform in DevOps.

## 🧠 1. What is a Container?

A container is a lightweight, standalone, executable unit that includes everything needed to run an application:

- Code
- Runtime
- System tools
- Libraries
- Settings

Unlike virtual machines, containers share the host OS kernel, making them faster and lighter.

## 🐳 2. What is Docker?

Docker is a containerization platform that helps you:

- Build container images
- Run containers
- Manage container lifecycle

🔍 Key Concepts:

| Term | Description |
| ---- | ----------- |
| Image | Blueprint (template) for a container |
| Container | Running instance of an image |
| Dockerfile | Script used to build a Docker image |
| Registry | Remote image store (e.g., Docker Hub, GitHub, Container Registry) |
| Volumes | Persistent storage for containers |
| Ports | Exposed services from container to host |

## 🔧 3. Install Docker

On Linux:

```bash
sudo apt update
sudo apt install docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER   # Use Docker without sudo
```

Check version:

```bash
docker --version
```

## 📘 4. Common Docker Commands

```bash
# Run a container (detached mode)
docker run -d -p 8080:80 nginx

# See running containers
docker ps

# Stop a container
docker stop <container_id>

# Remove a container
docker rm <container_id>

# Build an image from Dockerfile
docker build -t myapp:latest .

# Run container with a volume
docker run -v /host/data:/container/data myapp

# Execute command inside container
docker exec -it <container_id> bash

# View logs
docker logs <container_id>

# List images
docker images

# Push to Docker Hub
docker tag myapp yourdockerhubusername/myapp
docker push yourdockerhubusername/myapp
```

## 🛠️ 5. Write Your First Dockerfile

```Dockerfile
# Dockerfile for a simple Python app
FROM python:3.10

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

Build & Run:

```bash
docker build -t my-python-app .
docker run -p 5000:5000 my-python-app
```

## 📁 6. Volumes and Bind Mounts

Volumes:
Managed by Docker:

```bash
docker volume create myvol
docker run -v myvol:/data nginx
```

Bind Mount:
Use a local directory:

```bash
docker run -v $(pwd)/data:/data nginx
```

## 🔐 7. Docker Networking

By default, containers are on a shared bridge network.

```bash
docker network ls             # List networks
docker network create mynet  # Create a custom network
docker run --network=mynet myapp
```

This is helpful for connecting services like app + database in one network.

## 🧪 8. Practice Tasks (continued)

Here are hands-on challenges to strengthen your understanding:

### 🔹 Task 1: Run an Nginx container

```bash
docker run -d -p 8080:80 nginx
```

- ✅ Visit http://localhost:8080 to confirm it works.

- 🔄 Use docker stop and docker rm to clean up afterward.

### 🔹 Task 2: Containerize a Python Flask App

01. Create a simple Flask app:

    ```python
    # app.py
    from flask import Flask
    app = Flask(__name__)
    
    @app.route("/")
    def home():
        return "Hello from Docker!"
    
    if __name__ == "__main__":
        app.run(host="0.0.0.0", port=5000)
    ```

02. Add a requirements.txt:

    ```nginx
    flask
    ```

03. Write the Dockerfile:

    ```Dockerfile
    FROM python:3.10
    WORKDIR /app
    COPY requirements.txt .
    RUN pip install -r requirements.txt
    COPY . .
    CMD ["python", "app.py"]
    ```

04. Build and run:

    ```bash
    docker build -t flask-demo .
    docker run -p 5000:5000 flask-demo
    ```

    ✅ Visit http://localhost:5000

### 🔹 Task 3: Docker Compose a Multi-Container App

**Use Case:** Flask app + Redis

01. docker-compose.yml:

    ```yaml
    version: "3"
    services:
      web:
        build: .
        ports:
          - "5000:5000"
        depends_on:
          - redis
      redis:
        image: redis:alpine
    ```

02. Update app.py to use Redis:

    ```python
    import redis
    
    r = redis.Redis(host='redis', port=6379,     decode_responses=True)
    # store/retrieve keys in Flask routes
    ```

03. Run:

```bash
docker-compose up --build
```

## 📡 9. Docker Networking (Deeper Dive)

- Bridge (default): All standalone containers on this network.
- Host: Shares the host network stack (Linux only).
- Overlay: Used in Swarm to connect multiple Docker daemons.
- None: Isolated container, no networking.

You can inspect networks:

```bash
docker network inspect bridge
```

Create your own:

```bash
docker network create my-custom-net
```

Attach containers to it:

```bash
docker run --network=my-custom-net ...
```

## 📦 10. Image Optimization Tips

- Use smaller base images like `alpine` where possible.
- Minimize `RUN` steps to reduce layers.
- Clean up with `rm -rf` in Dockerfile to reduce image size.

Example:

```Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm ci --only=production
CMD ["node", "server.js"]
```

## 🔍 11. Debugging Containers

Attach shell:

```bash
docker exec -it <container_id> sh   # or bash
```

Inspect container:

```bash
docker inspect <container_id>
```

View logs:

```bash
docker logs <container_id>
```

## 🧠 12. Concepts Recap

| Concept | Purpose |
| ------- | ------- |
| Dockerfile | Blueprint for building images |
| Image | Read-only file system with app and dependencies |
| Container | Running instance of an image |
| Volume | Persist and share data |
| Network | Connect containers together |
| Registry | Store and pull images |

## 🧪 Self-Check Questions

- What is the difference between an image and a container?
- How does Docker handle networking between containers?
- How do you persist data between restarts?
- How would you debug a container that crashes on startup?
