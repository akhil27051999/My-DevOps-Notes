# 🐳 Docker Interview Questions


## 🧱 1. Docker Basics

1. What is Docker?
   - Docker is a containerization platform that packages applications with their dependencies into containers. It ensures consistency across environments.

2. How is Docker different from Virtual Machines?
   - Containers share the host OS kernel, making them lightweight and fast. VMs require full OS images with separate kernels, making them heavier.

3. What is the Docker architecture?
   - Key components: Docker Client, Docker Daemon, Docker Images, Docker Containers, Docker Registries.



## 📦 2. Docker Images & Containers

4. What is the difference between an Image and a Container?
   - Image: Blueprint (read-only).  
   - Container: Running instance (read-write) of the image.

5. How are Docker images built?
   - Using a Dockerfile and the `docker build` command.

6. What are image layers?
   - Each instruction in the Dockerfile creates a cached image layer that speeds up builds and reusability.



## ⚙️ 3. Dockerfile & Image Build

7. What are the common Dockerfile instructions?
   - `FROM`, `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, `ADD`, `ENV`, `EXPOSE`, `WORKDIR`, `VOLUME`.

8. What is the difference between CMD and ENTRYPOINT?
   - CMD provides default parameters, ENTRYPOINT defines the main command. ENTRYPOINT can't be easily overridden.

9. What is a multi-stage build?
   - A method to build lean production images by separating build and runtime environments in the Dockerfile.


## 📜 4. Docker Compose & Orchestration

10. What is Docker Compose?
    - A tool to define and run multi-container applications using a `docker-compose.yml` file.

11. What is the difference between Dockerfile and docker-compose.yml?
    - Dockerfile is for building images. Compose defines services and how containers work together.

12. What is the difference between Docker Compose and Docker Stack?
    - Compose: For local development.  
    - Stack: Used in production with Swarm mode, supports scaling and rolling updates.


## 🌐 5. Docker Networking

13. What are the different types of Docker networks?
    - `bridge`, `host`, `none`, `overlay`, and `macvlan`.

14. How does networking work between containers?
    - Containers can communicate if they share the same user-defined bridge network, using DNS resolution by container name.


## 🗃️ 6. Volumes & Data Management

15. What is the difference between volumes and bind mounts?
    - Volumes are managed by Docker and portable. Bind mounts use host paths and are not portable.

16. How are volumes created and used?
    - `docker volume create myvol`  
      `docker run -v myvol:/app/data myapp`

17. Why use volumes over storing data in containers?
    - Volumes persist data, are portable, efficient, and safer during container updates or removal.


## 🔐 7. Docker Security

18. How does Docker ensure container isolation?
    - By using Linux namespaces and control groups (cgroups).

19. What are best practices to secure Docker containers?
    - Use minimal base images, scan for vulnerabilities, run as non-root, restrict capabilities, and isolate networks.

20. What is the purpose of the .dockerignore file?
    - Prevents unnecessary files from being sent during image build (e.g., `.git`, `node_modules`).


## 🧼 8. Debugging & Logging

21. How can you debug a Docker container?
    - Use `docker logs`, `docker inspect`, `docker exec -it <container> sh` for interactive debugging.

22. How are container logs managed?
    - Through log drivers like `json-file`, `syslog`, or external log aggregators (e.g., ELK, Fluentd, Loki).


## 🗂️ 9. Docker Registries

23. What is a Docker registry and name a few?
    - A registry stores Docker images (public or private).  
      Examples: Docker Hub, GitHub Container Registry, AWS ECR, GCR.

24. How do you push/pull Docker images?
    - `docker push myapp:v1`  
      `docker pull myapp:v1`


## ⏱️ 10. Container Lifecycle

25. What is the lifecycle of a Docker container?
    - Image build → Container create → Start → Running → Stopped → Deleted.

26. What happens when a container is stopped?
    - The main process exits. The container is in `Exited` state until manually removed.


## 🧰 11. Advanced Docker Features

27. What are init containers?
    - Containers that run initialization logic (e.g., database migration) before the main app container starts.

28. What is a sidecar container?
    - A helper container that runs with the main container in the same Pod (used in Kubernetes too).

29. What are Docker labels and why are they useful?
    - Key-value pairs used to organize and manage Docker objects. Helpful in automation and monitoring.

30. What are Docker health checks?
    - Defined in the Dockerfile using `HEALTHCHECK` to monitor container health.


## 🚀 12. Docker Swarm & Scaling

31. What is Docker Swarm?
    - Docker’s native clustering tool for container orchestration and service scaling.

32. What are the benefits of using Docker Swarm?
    - High availability, service discovery, load balancing, rolling updates.

33. How do you scale services in Swarm?
    - Add `replicas: N` in Compose or run:  
      `docker service scale myservice=5`

34. How do you roll back services in Swarm?
    - Use `docker service update --rollback`


## 🛡️ 13. Secrets Management

35. How do you manage secrets in Docker?
    - Use `docker secret` in Swarm mode or pass environment variables securely using tools like Vault.

36. Why not store secrets in Docker images?
    - It violates security best practices. Secrets in images can be easily extracted.


### 📚 Tips for Interview

- Use real examples (`nginx`, `mysql`) to explain images and volumes.
- Relate concepts with analogies: Docker image = class, container = object.
- Know CI/CD pipeline use-cases: Docker with Jenkins, GitHub Actions, or Kubernetes.
- Always emphasize **security, optimization, and scalability**.


### ✅ Recommended Practice:  
 - Try building a full-stack app using Docker Compose.  
 - Use Alpine-based images and multistage builds.  
 - Implement health checks and secret management.

