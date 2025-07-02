
# 🐳 Dockerfile Syntax & Instruction Guide

A **Dockerfile** is a script that contains a series of instructions on how to build a Docker image.

---

## 🧱 Basic Structure

```Dockerfile
# 1. Base image
FROM ubuntu:22.04

# 2. Maintainer info (optional)
LABEL maintainer="you@example.com"

# 3. Set environment variables
ENV APP_ENV=production

# 4. Set working directory
WORKDIR /app

# 5. Copy files
COPY . /app

# 6. Install dependencies or run shell commands
RUN apt update && apt install -y python3

# 7. Expose ports
EXPOSE 8080

# 8. Define default command
CMD ["python3", "app.py"]
```

---

## 🧾 Common Instructions

| Instruction | Description | Example |
|-------------|-------------|---------|
| `FROM` | Sets base image | `FROM node:20-alpine` |
| `LABEL` | Metadata for image | `LABEL version="1.0"` |
| `ENV` | Set environment variables | `ENV NODE_ENV=production` |
| `WORKDIR` | Set working directory inside container | `WORKDIR /usr/src/app` |
| `COPY` | Copy files/directories from host | `COPY . .` |
| `ADD` | Like COPY but supports archives and URLs | `ADD https://... /file` |
| `RUN` | Execute shell command while building | `RUN apt-get update` |
| `CMD` | Default command to run on container start | `CMD ["npm", "start"]` |
| `ENTRYPOINT` | Run container as executable | `ENTRYPOINT ["java", "-jar", "app.jar"]` |
| `EXPOSE` | Inform Docker what port app listens on | `EXPOSE 80` |
| `ARG` | Define build-time variables | `ARG VERSION=1.0` |
| `VOLUME` | Mount a volume | `VOLUME /data` |
| `USER` | Set the user for RUN/CMD/ENTRYPOINT | `USER appuser` |

---

## 🆚 `CMD` vs `ENTRYPOINT`

| Feature | CMD | ENTRYPOINT |
|--------|-----|------------|
| Purpose | Default args | Executable path |
| Override | Yes via CLI | CMD adds args to ENTRYPOINT |
| Example | `CMD ["npm", "start"]` | `ENTRYPOINT ["python3"]` |

Combined:
```Dockerfile
ENTRYPOINT ["python3"]
CMD ["app.py"]
```
➡️ Becomes: `python3 app.py`

---

## 🔄 Multi-Stage Builds (to reduce image size)

```Dockerfile
FROM node:20 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

---

## 📌 Best Practices

✅ Use specific versions (e.g., `node:20-alpine` instead of `latest`)  
✅ Keep images small using multi-stage builds  
✅ Combine commands using `&&` to reduce layers  
✅ Clean up cache/temp files in `RUN`  
✅ Use `.dockerignore` to exclude unnecessary files  

---

## 📂 Example: Simple Python App Dockerfile

```Dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]
```

---

## 🔍 Debugging Build Failures

- Use `docker build --progress=plain` for verbose output
- Insert `RUN echo` steps to trace progress
- Add `RUN ls -al` and `cat` to check files mid-build

---

## 📚 Resources

- [Dockerfile Reference (Official)](https://docs.docker.com/engine/reference/builder/)
- [Best Practices for Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

---
