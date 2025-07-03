# 🐳 Complete Docker Concepts for Interview Preparation

## 📘 Core Concepts of Docker

| Concept            | Definition                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------ |
| **Docker**         | An open-source platform to build, ship, and run applications in containers.                |
| **Image**          | A lightweight, immutable file with application code, runtime, libraries, and dependencies. |
| **Container**      | A runtime instance of an image. It runs isolated from the host and other containers.       |
| **Dockerfile**     | A script with instructions to build a Docker image.                                        |
| **Docker Hub**     | A cloud-based registry to share Docker images.                                             |
| **Docker Engine**  | The runtime that builds and runs containers.                                               |
| **Volumes**        | Persistent data storage outside the container’s filesystem.                                |
| **Networks**       | Isolated communication layers for containers.                                              |
| **Docker Compose** | A tool for defining and running multi-container apps using `docker-compose.yml`.           |
| **Docker Stack**   | Docker Swarm deployment tool to deploy multi-service applications from a Compose file.     |


## 🏗️ Docker Architecture

* **Docker Client**: CLI to interact with Docker daemon.
* **Docker Daemon**: Core engine running in the background.
* **Docker Registries**: Stores and distributes images (e.g., Docker Hub).
* **Docker Objects**:

  * Images
  * Containers
  * Volumes
  * Networks


## 🔨 Most Important Docker Commands (Grouped)

### ✅ Image Commands

```bash
docker build -t image-name .             # Build image from Dockerfile
docker images                            # List local images
docker rmi image-id                      # Remove image
```

### ✅ Container Commands

```bash
docker run -d -p 8080:80 image-name      # Run container in detached mode
docker ps                                # List running containers
docker ps -a                             # List all containers
docker stop container-id                 # Stop running container
docker start container-id                # Start a stopped container
docker rm container-id                   # Remove a container
docker exec -it container-id bash        # Get interactive shell into container
docker logs container-id                 # View container logs
```

### ✅ Volume Commands

```bash
docker volume create myvol               # Create volume
docker run -v myvol:/app/data image      # Mount volume to container
docker volume ls                         # List volumes
```

### ✅ Network Commands

```bash
docker network create mynet              # Create custom network
docker network ls                        # List networks
docker network inspect bridge            # Inspect bridge network
```


## 📁 Dockerfile Directives

| Directive    | Purpose                                       |
| ------------ | --------------------------------------------- |
| `FROM`       | Base image to start with                      |
| `WORKDIR`    | Working directory inside the container        |
| `COPY`       | Copy files from host to container             |
| `RUN`        | Run shell commands during image build         |
| `CMD`        | Command to run at container startup           |
| `ENTRYPOINT` | Preferred command that doesn't get overridden |
| `EXPOSE`     | Declare container port to expose              |
| `ENV`        | Set environment variables                     |

### 🔧 Sample Dockerfile

```Dockerfile
FROM python:3.9
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```


## 🧱 Docker Compose

### 📘 What is Docker Compose?

Docker Compose is a tool for defining and managing multi-container Docker applications. It uses a YAML file (`docker-compose.yml`) to configure the application services, networks, and volumes.

### 🔧 Sample docker-compose.yml

```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app
    networks:
      - appnet

  redis:
    image: redis:alpine
    networks:
      - appnet

networks:
  appnet:
```

### ✅ Commands

```bash
docker-compose up -d                     # Start all services
docker-compose down                      # Stop and remove containers, networks, volumes
docker-compose ps                        # Show status of services
docker-compose logs                      # View logs for all services
docker-compose build                     # Build or rebuild services
```


## 🐝 Docker Stack (Swarm Mode)

### 📘 What is Docker Stack?

Docker Stack is used for deploying applications to a Docker Swarm cluster using a Compose file. It supports declarative service definitions and is used in production-scale container orchestration.

### 🔧 Sample docker-stack.yml

```yaml
version: '3.8'
services:
  web:
    image: myapp:latest
    ports:
      - "80:80"
    deploy:
      replicas: 3
      restart_policy:
        condition: on-failure
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

### ✅ Commands

```bash
docker swarm init                        # Initialize Docker Swarm mode
docker stack deploy -c docker-stack.yml mystack    # Deploy stack to swarm
docker stack ps mystack                 # View tasks in the stack
docker stack services mystack           # List running services
docker stack rm mystack                 # Remove the stack
```


## 🔍 Docker Use Cases

* Microservices architecture
* CI/CD pipelines (build, test, deploy stages)
* Isolated development environments
* Replicating production environments locally
* App portability across cloud and OS
* High availability deployment using Docker Swarm


## 🚨 Docker Troubleshooting

| Problem                    | Cause                                  | Fix                                        |
| -------------------------- | -------------------------------------- | ------------------------------------------ |
| Permission denied          | User not in docker group               | `sudo usermod -aG docker $USER` + relogin  |
| Image not found            | Wrong image name or tag                | Double-check `docker images` or Docker Hub |
| Port already in use        | Host port conflict                     | Use different port (e.g., `-p 8081:80`)    |
| Container exit immediately | CMD or ENTRYPOINT failure              | Check logs with `docker logs <id>`         |
| Build context too large    | Large unnecessary files                | Use `.dockerignore`                        |
| Swarm deployment failure   | Service not reachable or image missing | Inspect `docker service logs`              |


## 🧠 Docker Best Practices for Interviews

* Use **multi-stage builds** to optimize image size.
* Always define `.dockerignore` to exclude unnecessary files.
* Tag images with version (`v1.0`, `latest`) for clarity.
* Store sensitive data in **Docker secrets** (for Swarm).
* Use **healthchecks** in Dockerfile to define container health.
* Prefer Docker Compose for local dev and Docker Stack for production.

### ✅ Example: Multi-stage Dockerfile

```Dockerfile
FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```


