
# 🐳 Docker Command Reference with Arguments, Descriptions & Examples

---

## 1. Basic Docker Commands

| Command | Argument | Description | Example |
|---------|----------|-------------|---------|
| `docker --version` | – | Show Docker version installed. | `docker --version` |
| `docker info` | – | Show system-wide info: containers, images, storage driver, etc. | `docker info` |
| `docker help` | – | Show help for all Docker commands. | `docker help` |

---

## 2. Docker Images

| Command | Argument | Description | Example |
|---------|----------|-------------|---------|
| `docker pull` | `image[:tag]` | Download image from Docker Hub. | `docker pull nginx:latest` |
| `docker images` | `-a` | Show all images. | `docker images -a` |
|  | `--filter` | Filter image list. | `docker images --filter "dangling=true"` |
| `docker rmi` | `image_id` | Remove an image. | `docker rmi nginx:latest` |
| `docker build` | `-t name` | Tag image during build. | `docker build -t myapp:1.0 .` |
|  | `.` | Build context path. | `docker build .` |

---

## 3. Docker Containers

| Command | Argument | Description | Example |
|---------|----------|-------------|---------|
| `docker run` | `-d` | Run in background. | `docker run -d nginx` |
|  | `-it` | Interactive terminal. | `docker run -it ubuntu bash` |
|  | `--name` | Name the container. | `docker run --name webserver nginx` |
|  | `-p` | Port mapping. | `docker run -p 8080:80 nginx` |
|  | `-v` | Mount volume. | `docker run -v /data:/app/data nginx` |
|  | `--rm` | Remove on exit. | `docker run --rm ubuntu echo "Hello"` |
| `docker ps` | `-a` | Show all containers. | `docker ps -a` |
|  | `-q` | Show only IDs. | `docker ps -q` |
| `docker start` | `container_name/id` | Start container. | `docker start webserver` |
| `docker stop` | `container_name/id` | Stop container. | `docker stop webserver` |
| `docker restart` | `container_name/id` | Restart container. | `docker restart webserver` |
| `docker rm` | `container_name/id` | Remove container. | `docker rm webserver` |
| `docker exec` | `-it` | Interactive shell. | `docker exec -it webserver bash` |
|  | `command` | Command to run. | `docker exec webserver ls /usr/share/nginx/html` |
| `docker logs` | `-f` | Follow logs. | `docker logs -f webserver` |
|  | `--tail` | Show last N lines. | `docker logs --tail 100 webserver` |

---

## 4. Docker Volumes

| Command | Argument | Description | Example |
|---------|----------|-------------|---------|
| `docker volume create` | `volume_name` | Create volume. | `docker volume create data_vol` |
| `docker volume ls` | – | List volumes. | `docker volume ls` |
| `docker volume rm` | `volume_name` | Remove volume. | `docker volume rm data_vol` |
| In `docker run` | `-v` | Mount volume. | `docker run -v data_vol:/app/data nginx` |

---

## 5. Docker Networking

| Command | Argument | Description | Example |
|---------|----------|-------------|---------|
| `docker network ls` | – | List networks. | `docker network ls` |
| `docker network create` | `network_name` | Create network. | `docker network create my_net` |
| `docker network connect` | `network container` | Connect to network. | `docker network connect my_net webserver` |
| In `docker run` | `--network` | Use custom network. | `docker run --network my_net nginx` |

---

## 6. Dockerfile Instructions

| Instruction | Description | Example |
|-------------|-------------|---------|
| `FROM` | Base image. | `FROM node:18-alpine` |
| `COPY` | Copy files. | `COPY . /app` |
| `ADD` | Add files/archives. | `ADD archive.tar.gz /app` |
| `CMD` | Default command. | `CMD ["node", "server.js"]` |
| `ENTRYPOINT` | Executable container. | `ENTRYPOINT ["python3"]` |
| `EXPOSE` | Inform about ports. | `EXPOSE 3000` |
| `ENV` | Set environment variable. | `ENV NODE_ENV=production` |
| `WORKDIR` | Set working directory. | `WORKDIR /app` |

---

## 7. Docker Compose

| Command | Argument | Description | Example |
|---------|----------|-------------|---------|
| `docker-compose up` | `-d` | Detached mode. | `docker-compose up -d` |
|  | `--build` | Build before start. | `docker-compose up --build` |
| `docker-compose down` | – | Stop and remove. | `docker-compose down` |
| `docker-compose ps` | – | Show containers. | `docker-compose ps` |

---

## 8. Docker Cleanup

| Command | Argument | Description | Example |
|---------|----------|-------------|---------|
| `docker system prune` | `-a` | Remove all unused data. | `docker system prune -a` |
| `docker container prune` | – | Remove stopped containers. | `docker container prune` |
| `docker image prune` | – | Remove unused images. | `docker image prune` |
| `docker volume prune` | – | Remove unused volumes. | `docker volume prune` |

---

## 9. Example Summary

```bash
# Run nginx and expose port 8080
docker run -d -p 8080:80 --name webserver nginx

# Run interactive Ubuntu shell
docker run -it ubuntu bash

# Mount a volume
docker run -v /host/data:/container/data ubuntu ls /container/data

# Build image from Dockerfile
docker build -t myimage:v1 .

# Use Docker Compose
docker-compose up -d --build
```
