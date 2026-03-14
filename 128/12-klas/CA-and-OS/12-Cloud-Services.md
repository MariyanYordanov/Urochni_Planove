# УРОЧЕН ПЛАН №12
## УЧЕБНА ПРАКТИКА: КОМПЮТЪРНИ АРХИТЕКТУРИ И ОПЕРАЦИОННИ СИСТЕМИ
### XII КЛАС

---

## 1. ОСНОВНИ ДАННИ

- **Училище:** ПГИ „Професор д-р Асен Златаров"
- **Клас:** XII клас
- **Предмет:** Учебна практика: Компютърни архитектури и операционни системи
- **Тема на урока:** Docker контейнери - основи
- **Дата:** ____________
- **Час:** ____________
- **Продължителност:** 90 минути (2 учебни часа)
- **Тип урок:** Нови знания
- **Място на провеждане:** Компютърна лаборатория

---

## 2. ЦЕЛИ И ЗАДАЧИ

### ОБРАЗОВАТЕЛНИ ЦЕЛИ:
1. Учениците да разберат концепцията за контейнеризация
2. Да усвоят основните Docker концепции и терминология
3. Да научат основните Docker команди
4. Да разберат разликата между контейнери и виртуални машини
5. Да могат да работят с Docker images и containers

### ВЪЗПИТАТЕЛНИ ЦЕЛИ:
1. Формиране на разбиране за модерни DevOps практики
2. Възпитаване на ефективност при използване на ресурси
3. Развиване на интерес към cloud-native технологии
4. Изграждане на навици за автоматизация

### РАЗВИВАЩИ ЦЕЛИ:
1. Развитие на умения за работа с CLI
2. Усъвършенстване на системно мислене
3. Формиране на DevOps mindset
4. Развитие на способности за troubleshooting

---

## 3. СЪДЪРЖАНИЕ

### ОСНОВНИ ЗНАНИЯ И УМЕНИЯ:

#### Знания:
- Контейнеризация vs виртуализация
- Docker архитектура: daemon, client, registry
- Images, containers, volumes, networks
- Dockerfile синтаксис и best practices
- Docker Hub и registries
- Container lifecycle management

#### Умения:
- Инсталиране на Docker
- Работа с docker CLI
- Pulling и running containers
- Building custom images
- Managing container resources
- Basic networking и volumes

### ВРЪЗКИ С ДРУГИ ПРЕДМЕТИ:

1. **Linux администрация** - Linux namespaces, cgroups
2. **Програмиране** - application packaging
3. **Мрежи** - container networking, ports
4. **DevOps** - CI/CD pipelines
5. **Cloud computing** - microservices architecture

---

## 4. МЕТОДИ И СРЕДСТВА

### МЕТОДИ НА ПРЕПОДАВАНЕ:
1. **Интерактивна презентация** с демонстрации
2. **Практическа работа** с Docker CLI
3. **Live coding** на Dockerfile
4. **Сравнителен анализ** containers vs VMs
5. **Problem-based learning** с реални сценарии

### УЧЕБНИ СРЕДСТВА И МАТЕРИАЛИ:
1. **Софтуер:**
   - Docker Desktop / Docker Engine
   - Visual Studio Code
   - Terminal/PowerShell
   - Docker Hub account
   
2. **Хардуер:**
   - Компютри с Linux/Windows/macOS
   - Минимум 4GB RAM
   - Internet връзка
   
3. **Учебни материали:**
   - Docker документация
   - Примерни Dockerfiles
   - Cheat sheets

---

## 5. ХОД НА УРОКА

### **1. ОРГАНИЗАЦИОНЕН МОМЕНТ (5 минути)**

**Дейност на учителя:**
- Проверка на присъствието
- Проверка на Docker инсталацията
- Въвеждащ въпрос: "Защо да 'опаковаме' приложение в контейнер?"

**Дейност на учениците:**
- Проверка на Docker с `docker version`
- Подготовка на работна среда

### **2. АКТУАЛИЗАЦИЯ НА ЗНАНИЯТА (8 минути)**

**Дейност на учителя:**
- Преговор на виртуализация концепции

**Въпроси:**
1. Какво е виртуална машина?
2. Какви са недостатъците на VMs?
3. Какво е operating system kernel?
4. Защо портабилността е важна?

**The Problem Docker Solves:**
```
"But it works on my machine!"

Traditional deployment issues:
- Different environments
- Dependency conflicts  
- Version mismatches
- "Snowflake" servers
```

### **3. НОВ МАТЕРИАЛ (45 минути)**

#### **Част 1: Концепция за контейнеризация (10 мин)**

**Какво е контейнер?**
```
Container = Lightweight, standalone package
           containing everything needed to
           run software:
           - Code
           - Runtime
           - System tools
           - Libraries
           - Settings

Characteristics:
✓ Portable - runs anywhere
✓ Lightweight - shares OS kernel
✓ Isolated - separate processes
✓ Scalable - easy to replicate
✓ Ephemeral - disposable
```

**Containers vs Virtual Machines:**
```
Virtual Machines:          Containers:
┌──────────────┐          ┌──────────────┐
│     App A     │          │     App A     │
│   Guest OS    │          │   Libraries   │
├──────────────┤          ├──────────────┤
│     App B     │          │     App B     │
│   Guest OS    │          │   Libraries   │
├──────────────┤          ├──────────────┤
│   Hypervisor  │          │ Docker Engine │
├──────────────┤          ├──────────────┤
│    Host OS    │          │    Host OS    │
└──────────────┘          └──────────────┘

Size: GBs                  Size: MBs
Boot: Minutes              Boot: Seconds
Overhead: High             Overhead: Low
```

**Linux Technologies Behind Containers:**
```
Namespaces (isolation):
- PID: Process isolation
- NET: Network isolation
- MNT: Filesystem isolation
- UTS: Hostname isolation
- IPC: Inter-process communication
- USER: User isolation

Control Groups (cgroups):
- Memory limits
- CPU limits
- I/O limits
- Network bandwidth

Union Filesystems:
- Layered approach
- Copy-on-write
- Efficient storage
```

#### **Част 2: Docker архитектура (12 мин)**

**Docker Components:**
```
┌─────────────┐     ┌─────────────┐
│Docker Client│────▶│ Docker Host │
│  (docker)   │     │             │
└─────────────┘     │ ┌─────────┐ │
                    │ │ Docker  │ │
     API            │ │ Daemon  │ │
                    │ │(dockerd)│ │
                    │ └────┬────┘ │
                    │      │      │
                    │ ┌────▼────┐ │
                    │ │Containers│ │
                    │ └─────────┘ │
                    │ ┌─────────┐ │
                    │ │ Images  │ │
                    │ └─────────┘ │
                    └─────────────┘
                           │
                    ┌──────▼──────┐
                    │Docker Registry│
                    │ (Docker Hub)  │
                    └───────────────┘
```

**Key Concepts:**

**Images:**
```
- Read-only templates
- Layered filesystem
- Base image + changes
- Identified by name:tag
- Stored in registries

Example images:
nginx:latest
ubuntu:22.04
node:18-alpine
mysql:8.0
python:3.11-slim
```

**Containers:**
```
- Running instance of image
- Writable layer on top
- Isolated process
- Has lifecycle: create/start/stop/remove
- Can be committed to new image
```

**Registries:**
```
Docker Hub (default):
- Public registry
- Official images
- Community images
- Private repositories

Other registries:
- Amazon ECR
- Google Container Registry
- Azure Container Registry
- Self-hosted (Harbor, Nexus)
```

**Docker Commands Structure:**
```
docker <object> <command> <options>

Objects:
- container
- image
- network
- volume

Old syntax (still works):
docker run = docker container run
docker ps = docker container ls
docker images = docker image ls
```

#### **Част 3: Основни Docker команди (13 мин)**

**Working with Images:**
```bash
# Pull image from registry
docker pull nginx:latest

# List local images
docker images
docker image ls

# Inspect image
docker image inspect nginx

# Remove image
docker image rm nginx
docker rmi nginx

# Search Docker Hub
docker search nginx
```

**Running Containers:**
```bash
# Basic run
docker run nginx

# Run in background (detached)
docker run -d nginx

# Run with port mapping
docker run -d -p 8080:80 nginx

# Run with name
docker run -d --name webserver nginx

# Run interactively
docker run -it ubuntu bash

# Run with environment variables
docker run -e MYSQL_ROOT_PASSWORD=secret mysql

# Run with volume
docker run -v /host/path:/container/path nginx
```

**Container Management:**
```bash
# List running containers
docker ps
docker container ls

# List all containers
docker ps -a
docker container ls -a

# Stop container
docker stop webserver

# Start container
docker start webserver

# Restart container
docker restart webserver

# Remove container
docker rm webserver

# Force remove running container
docker rm -f webserver

# Execute command in running container
docker exec -it webserver bash

# View logs
docker logs webserver
docker logs -f webserver  # follow

# Inspect container
docker inspect webserver
```

**Practical Example - Run a Web Server:**
```bash
# 1. Pull nginx image
docker pull nginx:alpine

# 2. Run nginx container
docker run -d \
  --name my-nginx \
  -p 8080:80 \
  nginx:alpine

# 3. Check it's running
docker ps

# 4. Test with browser
# http://localhost:8080

# 5. View logs
docker logs my-nginx

# 6. Stop and remove
docker stop my-nginx
docker rm my-nginx
```

#### **Част 4: Dockerfile и building images (10 мин)**

**Dockerfile Basics:**
```dockerfile
# Dockerfile example for Node.js app

# Base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY . .

# Expose port
EXPOSE 3000

# Define startup command
CMD ["node", "app.js"]
```

**Dockerfile Instructions:**
```dockerfile
# FROM - base image
FROM ubuntu:22.04

# RUN - execute commands
RUN apt-get update && apt-get install -y nginx

# COPY - copy files from host
COPY ./app /usr/share/nginx/html

# ADD - copy files (with URL/tar support)
ADD https://example.com/file.tar.gz /tmp/

# WORKDIR - set working directory
WORKDIR /app

# ENV - environment variables
ENV NODE_ENV=production

# EXPOSE - document ports
EXPOSE 80 443

# CMD - default command
CMD ["nginx", "-g", "daemon off;"]

# ENTRYPOINT - executable
ENTRYPOINT ["python"]
CMD ["app.py"]

# VOLUME - mount point
VOLUME /data

# USER - run as user
USER appuser

# LABEL - metadata
LABEL version="1.0" maintainer="admin@example.com"
```

**Building Images:**
```bash
# Build image from Dockerfile
docker build -t myapp:1.0 .

# Build with specific Dockerfile
docker build -f Dockerfile.dev -t myapp:dev .

# Build with build args
docker build --build-arg VERSION=1.0 -t myapp .

# Multi-stage build example
```

**Multi-stage Build Example:**
```dockerfile
# Build stage
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### **4. ЗАТВЪРЖДАВАНЕ (27 минути)**

#### **Практическа работа: Docker hands-on**

**Упражнение 1: Run a Database (7 мин)**
```bash
# Run MySQL container
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=testdb \
  -e MYSQL_USER=user \
  -e MYSQL_PASSWORD=pass \
  -p 3306:3306 \
  mysql:8.0

# Connect to MySQL
docker exec -it mysql-db mysql -u root -p

# Inside MySQL:
SHOW DATABASES;
USE testdb;
EXIT;
```

**Упражнение 2: Build Custom Image (10 мин)**

Създайте simple web app:

**index.html:**
```html
<!DOCTYPE html>
<html>
<head>
    <title>My Docker App</title>
</head>
<body>
    <h1>Hello from Docker!</h1>
    <p>Student: [Your Name]</p>
</body>
</html>
```

**Dockerfile:**
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Build and Run:**
```bash
docker build -t my-web:1.0 .
docker run -d -p 8081:80 --name my-web my-web:1.0
# Open http://localhost:8081
```

**Упражнение 3: Docker Compose Preview (10 мин)**

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: app
    ports:
      - "3306:3306"
```

```bash
# Run with docker-compose
docker-compose up -d

# Stop services
docker-compose down
```

### **5. ОБОБЩЕНИЕ (10 минути)**

**Key Takeaways:**
```
Containers vs VMs:
✓ Lightweight
✓ Portable  
✓ Fast startup
✓ Resource efficient

Docker benefits:
✓ Consistent environments
✓ Easy deployment
✓ Scalability
✓ DevOps integration
```

**Real-world Use Cases:**
- Microservices architecture
- CI/CD pipelines
- Development environments
- Application modernization
- Cloud migration

**Container Best Practices:**
1. One process per container
2. Use official base images
3. Minimize layers
4. Don't run as root
5. Keep images small
6. Use .dockerignore
7. Tag images properly

### **6. ДОМАШНА РАБОТА (5 минути)**

**Задачи:**

1. **Практическа:**
   - Dockerize a simple application
   - Create 3-tier app (web, app, db)
   - Use docker-compose
   - Document the process

2. **Изследователска:**
   - Research Kubernetes
   - How does it relate to Docker?
   - Write 2-page comparison

3. **Project:**
   - Create personal portfolio site
   - Package in Docker container
   - Push to Docker Hub
   - Share link for review

**Срок:** До следващия учебен час

---

## 6. ОЦЕНЯВАНЕ

### КРИТЕРИИ ЗА ОЦЕНЯВАНЕ:

| Критерий | Точки |
|----------|-------|
| Разбиране на container концепции | 25% |
| Работа с Docker CLI | 25% |
| Building custom images | 20% |
| Dockerfile създаване | 15% |
| Troubleshooting умения | 10% |
| Активност | 5% |

### ОЦЕНЪЧНА РУБРИКА:
- **Отличен (6):** Създава сложни Dockerfiles, разбира multi-stage builds
- **Много добър (5):** Успешно работи с Docker, създава custom images
- **Добър (4):** Може да run и manage основни containers
- **Среден (3):** Разбира концепциите, нуждае се от помощ с командите

---

## 7. РЕФЛЕКСИЯ И АНАЛИЗ

### ВЪПРОСИ ЗА САМООЦЕНКА:
1. Разбирам ли разликата между image и container?
2. Мога ли да създам Dockerfile?
3. Умея ли да troubleshoot container проблеми?
4. Готов ли съм да използвам Docker в проекти?

### ИНДИКАТОРИ ЗА УСПЕХ:
- [ ] 95% разбират container концепцията
- [ ] 90% могат да run containers
- [ ] 85% създават basic Dockerfile
- [ ] 80% build custom images
- [ ] 75% използват volumes и networks

---

## 8. ПРИЛОЖЕНИЯ

### ПРИЛОЖЕНИЕ 1: DOCKER COMMAND CHEAT SHEET

**Essential Commands:**
```bash
# System
docker version          # Show version
docker info            # System info
docker system df       # Disk usage
docker system prune    # Clean up

# Images
docker images          # List images
docker pull IMAGE      # Download image
docker build -t TAG .  # Build image
docker push IMAGE      # Upload image
docker rmi IMAGE       # Remove image

# Containers
docker ps              # List running
docker ps -a           # List all
docker run IMAGE       # Run container
docker start ID        # Start stopped
docker stop ID         # Stop running
docker rm ID           # Remove container
docker exec -it ID sh  # Enter container
docker logs ID         # View logs
docker inspect ID      # Detailed info

# Cleanup
docker container prune # Remove stopped
docker image prune     # Remove unused
docker volume prune    # Remove unused volumes
docker network prune   # Remove unused networks
```

### ПРИЛОЖЕНИЕ 2: DOCKERFILE BEST PRACTICES

```dockerfile
# GOOD: Combine RUN commands
RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# BAD: Multiple RUN commands
RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get clean

# GOOD: Use specific versions
FROM node:18.17.1-alpine3.18

# BAD: Use latest
FROM node:latest

# GOOD: Copy specific files
COPY package*.json ./
RUN npm install
COPY . .

# BAD: Copy everything first
COPY . .
RUN npm install

# GOOD: Non-root user
RUN useradd -m appuser
USER appuser

# BAD: Run as root
# (default)
```

### ПРИЛОЖЕНИЕ 3: DOCKER-COMPOSE EXAMPLE

**Full Stack Application:**
```yaml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_API_URL=http://localhost:8000
    depends_on:
      - backend
    networks:
      - app-network

  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/mydb
      - REDIS_URL=redis://cache:6379
    depends_on:
      - db
      - cache
    networks:
      - app-network

  db:
    image: postgres:15
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=mydb
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - app-network

  cache:
    image: redis:7-alpine
    networks:
      - app-network

volumes:
  postgres_data:

networks:
  app-network:
    driver: bridge
```

---

**Изготвил:** [Име на учителя]  
**Дата на изготвяне:** Декември 2024 г.
