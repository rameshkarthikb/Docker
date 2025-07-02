
# 🐳 Docker Command Reference with Arguments and Descriptions

## 1. Basic Docker Commands

| Command | Argument | Description |
|---------|----------|-------------|
| `docker --version` | – | Show Docker version installed. |
| `docker info` | – | Show system-wide info: containers, images, storage driver, etc. |
| `docker help` | – | Show help for all Docker commands. |

---

## 2. Docker Images

| Command | Argument | Description |
|---------|----------|-------------|
| `docker pull` | `image[:tag]` | Download image from Docker Hub (e.g., `nginx:latest`). |
| `docker images` | `-a` | Show all images (default shows only active). |
|  | `--filter` | Filter output by label or dangling status. |
| `docker rmi` | `image_id` | Remove an image by ID or name. |
| `docker build` | `-t name` | Tags image with a name (e.g., `myapp:1.0`). |
|  | `.` | Path to Dockerfile context (usually `.` means current dir). |

---

## 3. Docker Containers

| Command | Argument | Description |
|---------|----------|-------------|
| `docker run` | `-d` | Run container in detached (background) mode. |
|  | `-it` | Interactive terminal (used for shell access). |
|  | `--name` | Assign a custom name to the container. |
|  | `-p host:container` | Map host port to container port (e.g., `8080:80`). |
|  | `-v host:container` | Mount volume (bind host directory to container). |
|  | `--rm` | Automatically remove container when it exits. |
| `docker ps` | `-a` | Show all containers (default shows only running). |
|  | `-q` | Show only container IDs (quiet mode). |
| `docker start` | `container_name/id` | Start a stopped container. |
| `docker stop` | `container_name/id` | Gracefully stop a running container. |
| `docker restart` | `container_name/id` | Restart a container. |
| `docker rm` | `container_name/id` | Remove a container. |
| `docker exec` | `-it` | Run command in container with interactive shell. |
|  | `container` | Target container name or ID. |
|  | `command` | Command to run (e.g., `bash`, `sh`). |
| `docker logs` | `-f` | Follow log output (streaming). |
|  | `--tail n` | Show only last n lines of logs. |

---

## 4. Docker Volumes

| Command | Argument | Description |
|---------|----------|-------------|
| `docker volume create` | `volume_name` | Create a new named volume. |
| `docker volume ls` | – | List all volumes. |
| `docker volume rm` | `volume_name` | Remove a volume. |
| In `docker run` | `-v volume_name:/path` | Mount volume into container. |

---

## 5. Docker Networking

| Command | Argument | Description |
|---------|----------|-------------|
| `docker network ls` | – | List all networks. |
| `docker network create` | `network_name` | Create a custom network. |
| `docker network connect` | `network container` | Attach container to a network. |
| In `docker run` | `--network` | Specify custom network to use. |

---

## 6. Dockerfiles (Build-time Arguments)

| Dockerfile Instruction | Description |
|------------------------|-------------|
| `FROM` | Base image (e.g., `ubuntu`, `node`). |
| `COPY` | Copy files from host to container image. |
| `ADD` | Like COPY but supports URLs and archive unpacking. |
| `CMD` | Default command to run when container starts. |
| `ENTRYPOINT` | Configure container to run as executable. |
| `EXPOSE` | Inform Docker of ports the container listens on. |
| `ENV` | Set environment variables. |
| `WORKDIR` | Set working directory inside container. |

---

## 7. Docker Compose

| Command | Argument | Description |
|---------|----------|-------------|
| `docker-compose up` | `-d` | Run services in detached mode. |
|  | `--build` | Build images before starting containers. |
| `docker-compose down` | – | Stop and remove containers/networks. |
| `docker-compose ps` | – | List running containers from Compose. |

---

## 8. Docker Cleanup

| Command | Argument | Description |
|---------|----------|-------------|
| `docker system prune` | `-a` | Remove all unused images, containers, volumes, networks. |
| `docker container prune` | – | Remove stopped containers. |
| `docker image prune` | – | Remove unused images. |
| `docker volume prune` | – | Remove unused volumes. |

---

## 9. Example Commands

```bash
# Run nginx and expose port 8080 on host
docker run -d -p 8080:80 --name webserver nginx

# Run interactive Ubuntu shell
docker run -it ubuntu bash

# Run with mounted volume
docker run -v /host/data:/container/data ubuntu ls /container/data

# Build image from Dockerfile with tag
docker build -t myimage:v1 .
```
