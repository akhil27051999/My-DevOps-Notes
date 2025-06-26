# 🐳 Complete Docker Concepts for Interview Preparation (99% Coverage)

This section covers everything you need to master Docker for interviews—concepts, commands, architecture, use cases, troubleshooting, and most-asked interview questions.

---

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

---

## 🏗️ Docker Architecture

* **Docker Client**: CLI to interact with Docker daemon.
* **Docker Daemon**: Core engine running in the background.
* **Docker Registries**: Stores and distributes images (e.g., Docker Hub).
* **Docker Objects**:

  * Images
  * Containers
  * Volumes
  * Networks

---

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

---

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

---

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

---

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

---

## 🔍 Docker Use Cases

* Microservices architecture
* CI/CD pipelines (build, test, deploy stages)
* Isolated development environments
* Replicating production environments locally
* App portability across cloud and OS
* High availability deployment using Docker Swarm

---

## 🚨 Docker Troubleshooting

| Problem                    | Cause                                  | Fix                                        |
| -------------------------- | -------------------------------------- | ------------------------------------------ |
| Permission denied          | User not in docker group               | `sudo usermod -aG docker $USER` + relogin  |
| Image not found            | Wrong image name or tag                | Double-check `docker images` or Docker Hub |
| Port already in use        | Host port conflict                     | Use different port (e.g., `-p 8081:80`)    |
| Container exit immediately | CMD or ENTRYPOINT failure              | Check logs with `docker logs <id>`         |
| Build context too large    | Large unnecessary files                | Use `.dockerignore`                        |
| Swarm deployment failure   | Service not reachable or image missing | Inspect `docker service logs`              |

---

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

## ❓ Docker Interview Questions with Answers

1. **What is Docker and how is it different from virtual machines?**

   * Docker is a containerization tool that packages apps and dependencies together. Unlike VMs, it shares the host OS kernel, making containers lightweight and faster to start.

2. **What is the difference between a Docker image and a container?**

   * An image is a blueprint (read-only); a container is a running instance (read-write) created from the image.

3. **Explain how Docker handles networking.**

   * Docker supports bridge, host, overlay, and macvlan networks. Each container gets an IP address, and `docker network` is used to manage communication.

4. **How does a Dockerfile differ from a docker-compose file?**

   * Dockerfile defines how to build an image. Docker Compose defines how to run multi-container applications.

5. **What is a volume and how is it used in Docker?**

   * Volumes persist data beyond container lifecycle. They are mounted into containers using `-v` or `--mount`.

6. **What are the different types of Docker networks?**

   * `bridge` (default), `host`, `none`, `overlay`, and `macvlan`. Each is suited for different use cases.

7. **Explain the difference between CMD and ENTRYPOINT.**

   * `CMD` sets default commands. `ENTRYPOINT` defines the main command that runs and cannot be overridden easily.

8. **What are the layers in a Docker image?**

   * Each Dockerfile instruction creates a new layer. Layers are cached and reused to optimize builds.

9. **What is a Docker registry? Can you name some?**

   * A registry is where Docker images are stored and retrieved. Examples: Docker Hub, GitHub Container Registry, AWS ECR.

10. **How can you reduce the size of a Docker image?**

    * Use smaller base images (e.g., Alpine), clean up packages, use multi-stage builds, and minimize layers.

11. **How do you debug a container that is crashing repeatedly?**

    * Use `docker logs`, `docker inspect`, and `docker exec` to check logs, configuration, and connect interactively.

12. **What’s the role of `.dockerignore`?**

    * It prevents unnecessary files (e.g., `.git`, `node_modules`) from being included in the build context.

13. **What is the difference between bind mounts and volumes?**

    * Bind mounts map host paths. Volumes are managed by Docker and offer portability and better performance.

14. **How does Docker ensure isolation of containers?**

    * Using Linux namespaces (PID, mount, network) and cgroups for resource limits.

15. **What is the purpose of multi-stage builds?**

    * To separate build environment from runtime, resulting in smaller, secure images.

16. **How do you secure Docker containers in production?**

    * Use non-root users, scan images, limit capabilities, apply network rules, and use Docker Bench for security.

17. **What happens when a container is stopped?**

    * The process stops, and container is marked as `Exited`. Data in memory is lost, unless volumes are used.

18. **How do you manage container logs?**

    * `docker logs`, log drivers (json-file, syslog, fluentd, etc.). Use centralized tools like ELK or Loki.

19. **Can you explain the lifecycle of a Docker container?**

    * Build image → Run container → Execute process → Stop → Remove (optional)

20. **How do you handle secrets in Docker?**

    * In Swarm mode, use `docker secret`. For Compose, use environment variables or third-party tools like HashiCorp Vault.

21. **What is Docker Stack and how does it differ from Compose?**

    * Docker Stack uses `docker-compose.yml` for deploying apps in Swarm. It supports service-level scaling and rolling updates.

22. **What are the benefits of using Docker Swarm over Compose in production?**

    * Compose is local; Swarm is distributed. Swarm enables clustering, service scaling, load balancing, and fault tolerance.

23. **How do you scale a service using Docker Stack?**

    * Use `deploy.replicas` in the YAML or run: `docker service scale service_name=5`

24. **How do you roll back a failed deployment in Docker Stack?**

    * `docker service update --rollback` reverts the service to its last working state.
