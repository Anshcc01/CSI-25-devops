
# 🚢 Docker Fundamentals & Hands-on Guide

This guide walks you through the fundamentals of Docker, covering everything from basic commands to multi-container applications using Docker Compose. Each section includes clear steps and associated resources for deeper understanding.

---

## 📦 1. Introduction to Containerization and Docker Fundamentals

### Steps:
- Understand what containers and Docker are.
- Learn differences between VMs and containers.
- Get familiar with Docker architecture (client, daemon, images, containers).

### Resources:
- 📺 [YouTube Video](https://www.youtube.com/watch?v=jPdIRX6q4jA)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 🧰 2. Docker Installation and Basic Container Operations

### Steps:
- Install Docker [Get Docker](https://docs.docker.com/get-docker/)
- Run your first container:  
  ```bash
  docker run hello-world
  docker ps
  docker ps -a
  docker stop <container_id>
  docker rm <container_id>
  docker rmi <image_id>
  ```

### Resources:
- 📺 [YouTube Video](https://youtu.be/LQjaJINkQXY?si=5nHnY6Bf2O9DRS-H)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 🏗️ 3. Build an Image from Dockerfile

### Steps:
- Create a `Dockerfile`:
  ```Dockerfile
  FROM ubuntu
  RUN apt-get update && apt-get install -y curl
  CMD ["bash"]
  ```
- Build and run:
  ```bash
  docker build -t myubuntu .
  docker run -it myubuntu
  ```

### Resources:
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 🗃️ 4. Docker Registry, DockerHub, Multi-Stage Build

### Steps:
- Login to DockerHub:
  ```bash
  docker login
  ```
- Multi-stage example `Dockerfile`:
  ```Dockerfile
  FROM node:18 AS builder
  WORKDIR /app
  COPY . .
  RUN npm install && npm run build

  FROM nginx:alpine
  COPY --from=builder /app/build /usr/share/nginx/html
  ```

### Resources:
- 📺 [YouTube Video](https://youtu.be/VyO8MPIfHnE?si=jznsWRY8rzEqmGDZ)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 🏗️ 5. Create Docker Images (Dockerfile & from Containers)

### Methods:
1. **Using Dockerfile** (as above)
2. **From running container:**
   ```bash
   docker commit <container_id> mycustomimage
   ```

### Resources:
- 📺 [YouTube Video](https://www.youtube.com/watch?v=apGV9Kg7ics)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 🔁 6. Push and Pull Images to Docker Hub & ACR

### DockerHub:
```bash
docker tag mycustomimage username/myimage:v1
docker push username/myimage:v1
docker pull username/myimage:v1
```

### Azure Container Registry (ACR):
```bash
az acr login --name <registryName>
docker tag myimage <registryName>.azurecr.io/myimage:v1
docker push <registryName>.azurecr.io/myimage:v1
```

### Resources:
- 📺 [YouTube Video](https://www.youtube.com/watch?v=b_euX_M82uI)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 🌐 7. Create a Custom Docker Bridge Network

### Steps:
```bash
docker network create --driver bridge mycustomnetwork
docker run -d --name app1 --network mycustomnetwork nginx
docker run -d --name app2 --network mycustomnetwork nginx
```

### Resources:
- 📺 [YouTube Video](https://www.youtube.com/watch?v=c6Ord0GAOp8&pp=ygURZG9ja2VyIG5ldHdvcmtpbmc%3D)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 💾 8. Create a Docker Volume and Mount it

### Steps:
```bash
docker volume create mydata
docker run -d --name db --mount source=mydata,target=/data busybox
```

### Resources:
- 📺 [YouTube Video](https://www.youtube.com/watch?v=u_0O4DOo2GI&pp=ygUOZG9ja2VyIHN0b3JhZ2U%3D)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## 🧩 9. Docker Compose & Security Best Practices

### Compose Example (`docker-compose.yml`):
```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  redis:
    image: redis
```
```bash
docker-compose up
```

### Docker Security Best Practices:
- Use official base images.
- Scan images for vulnerabilities.
- Run as non-root user.
- Limit container privileges.

### Resources:
- 📺 [YouTube Video](https://www.youtube.com/watch?v=HG6yIjZapSA&pp=ygUNZG9ja2UgY29tcG9zZQ%3D%3D)  
- 📘 [Docker Curriculum](https://docker-curriculum.com/)

---

## ✅ Summary

| Topic                              | Key Command / Tool              |
|-----------------------------------|----------------------------------|
| Install Docker                    | `docker run hello-world`        |
| Build from Dockerfile             | `docker build`                  |
| DockerHub Push/Pull               | `docker push`, `docker pull`    |
| Multi-Stage Build                 | `COPY --from=`                  |
| Custom Network                    | `docker network create`         |
| Docker Volumes                    | `docker volume create`          |
| Docker Compose                    | `docker-compose up`             |

---

> ✨ Explore [https://docker-curriculum.com](https://docker-curriculum.com/) for an in-depth hands-on walkthrough!
