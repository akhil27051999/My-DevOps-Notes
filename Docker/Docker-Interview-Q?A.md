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
